# Changing node versions automatically when I cd into a project

PS: This method just works on Mac.

Step 1: install nvm.
```
npm i -g nvm
```

Step2: install node versions.
```
nvm install v12.16.0
nvm install v17.3.0
```

Step3: switch node version as default.
```
nvm use v12.16.0
```

Step4: modify ~/.zshrc and restart terminal.
```
# place this after nvm initialization!
autoload -U add-zsh-hook
load-nvmrc() {
  local node_version="$(nvm version)"
  local nvmrc_path="$(nvm_find_nvmrc)"

  if [ -n "$nvmrc_path" ]; then
    local nvmrc_node_version=$(nvm version "$(cat "${nvmrc_path}")")

    if [ "$nvmrc_node_version" = "N/A" ]; then
      nvm install
    elif [ "$nvmrc_node_version" != "$node_version" ]; then
      nvm use
    fi
  elif [ "$node_version" != "$(nvm version default)" ]; then
    echo "Reverting to nvm default version"
    nvm use default
  fi
}
add-zsh-hook chpwd load-nvmrc
load-nvmrc
```

Step5: add `.nvmrc` file to the project.
```
v17.3.0
```

Now when you cd into the project, you can see the node version automatically changed.