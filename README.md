## 🧰 Install kubectx, kubens, and fzf with Oh-My-Zsh, Powerlevel10k

> ✅ This setup is tested and compatible with the following OS versions:
>
> | OS Version   | Compatibility     |
> | ------------ | ----------------- |
> | macOS (Intel/ARM)| ✅ Fully Supported |
>
> All tools used here (kubectx, kubens, fzf, oh-my-zsh, and Powerlevel10k) work seamlessly on these platforms without modification.
### 1. Install Homebrew Package Manager for macOS
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew -v
```
### 2. Install Git 
```bash
brew install git
git --version
```
### 1. Install Oh My ZSH
```bash
brew install zsh
zsh --version
```
### 1. Install kubectx, kubens, and fzf

```bash
sudo git clone https://github.com/ahmetb/kubectx /opt/kubectx
sudo ln -s /opt/kubectx/kubectx /usr/local/bin/kubectx
sudo ln -s /opt/kubectx/kubens /usr/local/bin/kubens

# Install fzf
sudo apt install fzf -y
```

---

### 2. Set up Aliases in Shell Config

#### For Zsh:

Open `.zshrc`:

```bash
vi ~/.zshrc
```

Add:

```zsh
# kubectx and kubens shortcut aliases
alias ktx='kubectx'
alias kns='kubens'
alias k='kubectl'
```

#### For Bash:

Open `.bashrc`:

```bash
vi ~/.bashrc
```

Add:

```bash
# kubectx and kubens shortcut aliases
alias ktx='kubectx'
alias kns='kubens'
alias k='kubectl'
```

---

### 3. Enable Auto-completion for kubectx and kubens

#### For Zsh:

```zsh
# kubectx/kubens completion for zsh
source <(kubectx completion zsh)
source <(kubens completion zsh)
```

#### For Bash:

```bash
# kubectx/kubens completion for bash
source <(kubectx completion bash)
source <(kubens completion bash)
```

---

### 4. Install fzf with full feature support

```bash
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
~/.fzf/install
```

Select `yes` for all prompts to enable key-bindings and completion.

---

### 5. Add fzf-based ktx/kns Functions

#### For Zsh (`~/.zshrc`):

```zsh
# Fuzzy kubectx with fzf
function ktx() {
  local ctx
  ctx=$(kubectx | fzf --prompt="K8s Context> " --height=40%) && kubectx "$ctx"
}

# Fuzzy kubens with fzf
function kns() {
  local ns
  ns=$(kubens | fzf --prompt="Namespace> " --height=40%) && kubens "$ns"
}
```

#### For Bash (`~/.bashrc`):

```bash
# Fuzzy kubectx with fzf
ktx() {
  local ctx
  ctx=$(kubectx | fzf --prompt="K8s Context> " --height=40%) && kubectx "$ctx"
}

# Fuzzy kubens with fzf
kns() {
  local ns
  ns=$(kubens | fzf --prompt="Namespace> " --height=40%) && kubens "$ns"
}
```

---

### 6. Reload the Shell

#### Zsh:

```bash
source ~/.zshrc
```

#### Bash:

```bash
source ~/.bashrc
```

---

### 7. Test the Shortcuts

* Run `ktx` to interactively switch Kubernetes contexts
* Run `kns` to interactively switch namespaces

#### You can test with the following steps:

```bash
# Check if ktx lists contexts properly
ktx
# Select a context and confirm it has switched
kubectl config current-context

# Check if kns lists namespaces properly
kns
# Confirm active namespace by running:
kubectl config view --minify | grep namespace
```

---

### 8. (Optional) Install k9s - Terminal UI for Kubernetes

`k9s` is a powerful terminal-based UI to manage Kubernetes clusters more interactively.

#### Install k9s (Latest Binary Method):

```bash
curl -sSLo k9s.tar.gz https://github.com/derailed/k9s/releases/latest/download/k9s_Linux_amd64.tar.gz
mkdir -p ~/.local/bin && tar -xzf k9s.tar.gz -C ~/.local/bin
chmod +x ~/.local/bin/k9s
```

#### Add to PATH:

##### For Bash:

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

##### For Zsh:

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

#### Or Install via Homebrew (on macOS/Linux):

```bash
brew install k9s
```

Then simply run:

```bash
k9s
```

`k9s` is a powerful terminal-based UI to manage Kubernetes clusters more interactively.

#### Install k9s (Latest Binary Method):

```bash
curl -sSLo k9s.tar.gz https://github.com/derailed/k9s/releases/latest/download/k9s_Linux_amd64.tar.gz
mkdir -p ~/.local/bin && tar -xzf k9s.tar.gz -C ~/.local/bin
chmod +x ~/.local/bin/k9s
```

Add to your PATH if not already:

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc  # or ~/.zshrc
```

#### Or Install via Homebrew (on macOS/Linux):

```bash
brew install k9s
```

Then simply run:

```bash
k9s
```

---

### 🔗 Reference Links

* kubectx & kubens: [https://github.com/ahmetb/kubectx](https://github.com/ahmetb/kubectx)
* fzf: [https://github.com/junegunn/fzf](https://github.com/junegunn/fzf)

