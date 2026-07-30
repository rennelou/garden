Guia de Montagem: Arch Linux + Hyprland (Otimizado)
1. Fundação do Sistema (Arch + BTRFS)
A. Preparação da Rede e Chroot

    Conexão: Use o celular (Tethering USB) para internet inicial.

    Drivers:
    Bash

pacman -Sy archlinux-keyring
pacman -S base-devel linux-headers git dkms usb_modeswitch
git clone https://aur.archlinux.org/rtl8852au-dkms-git.git
cd rtl8852au-dkms-git && makepkg -si

Particionamento: (SSD: sda1 EFI, sda2 BTRFS | HDD: sdb1 BTRFS).

Montagem (BTRFS):
Bash

    # SSD
    mkfs.fat -F32 /dev/sda1
    mkfs.btrfs /dev/sda2
    mount /dev/sda2 /mnt
    btrfs subvolume create /mnt/@
    btrfs subvolume create /mnt/@home
    btrfs subvolume create /mnt/@snapshots
    umount /mnt
    mount -o subvol=@,compress=zstd /dev/sda2 /mnt
    mkdir -p /mnt/{boot,home,.snapshots,mnt/hdd}
    mount /dev/sda1 /mnt/boot
    mount -o subvol=@home,compress=zstd /dev/sda2 /mnt/home
    mount -o subvol=@snapshots,compress=zstd /dev/sda2 /mnt/.snapshots

    # HDD
    mkfs.btrfs /dev/sdb1
    mount -o compress=zstd:1,autodefrag,noatime /dev/sdb1 /mnt/mnt/hdd

2. Instalação e Login (Otimizado)
A. Pacotes Base
Bash

pacstrap /mnt base linux linux-firmware base-devel nano networkmanager nix-ld greetd tuigreet hyprland

B. Configuração do greetd (Login sem bloat)

Edite /etc/greetd/config.toml:
Ini, TOML

[default_session]
command = "tuigreet --time --cmd 'Hyprland'"
user = "greeter"

Ative no systemd: systemctl enable --now greetd
3. Kit de Usabilidade "Windows-User"

Instale estas ferramentas após o primeiro boot:
Bash

sudo pacman -S waybar wofi network-manager-applet blueman thunar swappy mako pamixer wob swww

4. Configuração Visual (O "Wow" Factor)
A. Launcher (Wofi em modo Grid)

No seu ~/.config/wofi/config:
Plaintext

show=drun
allow_images=true
columns=4
width=500
height=400

B. Wallpaper e Mascote (Jujutsu Kaisen)

    Wallpaper:
    Bash

    swww init
    swww img path/to/seu_gif_ou_webp.gif

    Widget (AGS):

        Clone o repositório do ags.

        Crie um widget que carregue um GIF do personagem escolhido em um container Box com vertical layout.

        Adicione o calendário (código disponível no wiki do AGS) para aparecer ao clicar na data da Waybar.

C. Atalhos no hyprland.conf

Adicione estas binds para criar a experiência de "Windows-User":
Ini, TOML

# Menu (Wofi)
bind = SUPER, A, exec, wofi --show drun

# Screenshot (Swappy)
bind = , PRINT, exec, grim -g "$(slurp)" - | swappy -f -

# Volume (Wob)
bind = , XF86AudioRaiseVolume, exec, pamixer -i 5 && pamixer --get-volume > $XDG_RUNTIME_DIR/wob.sock
bind = , XF86AudioLowerVolume, exec, pamixer -d 5 && pamixer --get-volume > $XDG_RUNTIME_DIR/wob.sock

# Gerenciador de Arquivos
bind = SUPER, E, exec, thunar

5. Estratégia de Compartilhamento (Dicas para o Casal)

    Pastas Separadas: Cada usuário tem sua ~/.config/hypr/. Você pode ter um arquivo hyprland.conf minimalista, e a sua namorada um com animações, temas claros e o widget de Jujutsu Kaisen.

    Dados Comuns: Use a pasta /mnt/hdd (que montamos) para salvar documentos, fotos e jogos. Ambos os usuários devem ter permissão de escrita nesta partição.

    Ambiente de Pesquisa: Sempre que você for pesquisar, crie o flake.nix e use nix develop dentro da pasta do projeto. O sistema permanecerá imaculado para o uso diário dela.

Dica Final: Se o PC estiver travando ou o hardware estiver pesado, use o Ctrl+Alt+F2 para ir a um terminal puro, logar e verificar o uso de RAM com o comando free -h. O Arch com esse setup deve consumir menos de 500MB de RAM logo após o boot.
