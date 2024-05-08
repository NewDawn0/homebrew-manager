# Homebrew manager
A homebrew installer/remover cli

## Installation
### Imperatively
```bash
git clone https://github.com/NewDawn0/homebrew-manager
nix profile install .
```
### Declaratively
1. Add it as an input to your system flake as follows
    ```nix
    {
      inputs = {
        # Your other inputs ...
        homebrew-manager = {
          url = "github:NewDawn0/homebrew-manager";
          inputs.nixpkgs.follows = "nixpkgs";
          # Optional: If you use nix-systems or rust-overlay
          inputs.nix-systems.follows = "nix-systems";
        };
      };
    }
    ```
2. Add this to your overlays to expose shell-utils to your pkgs
    ```nix
    (final: prev: {
      homebrew-manager = inputs.homebrew-manager.packages.${prev.system}.default;
    })
    ```
3. Then you can either install it in your `environment.systemPackages` using 
    ```nix
    environment.systemPackages = with pkgs; [ homebrew-manager ];
    ```
    or install it to your `home.packages`
    ```nix
    home.packages = with pkgs; [ homebrew-manager ];
    ```