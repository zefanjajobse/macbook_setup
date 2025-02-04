# project to setup my laptop
before running, a few tools have to be installed
```sh
xcode-select --install
# brew to manage package installs
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
# python via pyenv, so it can easily be upgraded without much work. and to keep the default mac-os python clean
# with the dependencies to build python within pyenv
brew install pyenv openssl readline sqlite3 xz zlib tcl-tk@8
# add python to path
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo '[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(pyenv init - zsh)"' >> ~/.zshrc
# Install the latest version of python
pyenv install 3.12
# install poetry
curl -sSL https://install.python-poetry.org | python3 -
# automatically use .env when using poetry install
poetry config virtualenvs.in-project true
# install requirements
poetry run ansible-galaxy install -r requirements.yml     
# run the playbook
poetry run ansible-playbook main.yml --ask-become-pass
```