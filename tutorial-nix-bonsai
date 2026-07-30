Use este guia dentro de qualquer pasta de projeto. Ele garante que seu Python acesse a GPU via nix-ld sem poluir o Arch.
1. Criar o Flake do Projeto (flake.nix)

Crie este arquivo na raiz da pasta da sua pesquisa:
{
  description = "Ambiente RL isolado com acesso à GPU via nix-ld";
  inputs = { nixpkgs.url = "github:NixOS/nixpkgs/nixos-unstable"; };
  outputs = { self, nixpkgs }:
  let
    system = "x86_64-linux";
    pkgs = import nixpkgs { inherit system; config.allowUnfree = true; };
  in {
    devShells.${system}.default = pkgs.mkShell {
      buildInputs = with pkgs; [ python311 python311Packages.pip python311Packages.virtualenv ];
      # A Mágica: nix-ld permite que o Python dentro do Nix acesse as libs de GPU no Arch
      shellHook = ''
        export LD_LIBRARY_PATH=/usr/lib:${pkgs.stdenv.cc.cc.lib}/lib:$LD_LIBRARY_PATH
        if [ ! -d ".venv" ]; then python -m venv .venv; fi
        source .venv/bin/activate
        pip install --upgrade pip
      '';
    };
  };
}

2. Validação de Hardware (validate_hw.py)

Crie este arquivo na pasta do projeto e execute-o sempre que subir o ambiente:

import torch
print(f"=== VALIDAÇÃO DE HARDWARE ===")
if torch.cuda.is_available():
    print(f"[SUCESSO] GPU Identificada: {torch.cuda.get_device_name(0)}")
else:
    print("[ERRO] GPU não detectada. Nix-LD pode estar mal configurado.")

3. Instalação e Execução do Bonsai

Dentro do ambiente ativado (nix develop):

# Instalar bibliotecas de suporte
pip install torch torchvision torchaudio transformers accelerate huggingface_hub

# Login Hugging Face
huggingface-cli login

# Rodar inferência do Bonsai
# (Script de exemplo para carregar o modelo da coleção prism-ml/bonsai)
python -c "
from transformers import AutoModelForCausalLM
# Substitua pelo ID real que deseja testar
model = AutoModelForCausalLM.from_pretrained('prism-ml/bonsai-1', device_map='auto')
print('Modelo Bonsai carregado na GPU com sucesso!')
"

