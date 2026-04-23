# 1. Добавляем официальный GPG-ключ OpenTofu
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://get.opentofu.org/opentofu.gpg | sudo tee /etc/apt/keyrings/opentofu.gpg >/dev/null
curl -fsSL https://packages.opentofu.org/opentofu/tofu/gpgkey | sudo gpg --no-tty --batch --dearmor -o /etc/apt/keyrings/opentofu-repo.gpg >/dev/null

sudo chmod a+r /etc/apt/keyrings/opentofu.gpg /etc/apt/keyrings/opentofu-repo.gpg

# 2. Добавляем репозиторий OpenTofu
echo \
  "deb [signed-by=/etc/apt/keyrings/opentofu.gpg,/etc/apt/keyrings/opentofu-repo.gpg] https://packages.opentofu.org/opentofu/tofu/any/ any main" | \
  sudo tee /etc/apt/sources.list.d/opentofu.list

# 3. Обновляем пакеты и устанавливаем OpenTofu
sudo apt update
sudo apt install -y tofu

# 4. Проверяем версию (должна быть >=1.12, обычно 1.9.x)
tofu --version

# 1. Устанавливаем snapd 
sudo apt update

sudo apt install -y snapd

# 2. Устанавливаем Terraform через snap (классический канал — свежие версии)
sudo snap install terraform --classic

# 3. Проверяем версию
terraform --version


# 1. Обновляем систему
sudo apt update && sudo apt upgrade -y

# 2. Устанавливаем необходимые утилиты
sudo apt install -y ca-certificates curl gnupg lsb-release

# 3. Создаём папку для ключей и добавляем официальный GPG-ключ Docker
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# 4. Добавляем официальный репозиторий Docker
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# 5. Обновляем список пакетов ещё раз
sudo apt update

# 6. Устанавливаем Docker + docker-compose-plugin + containerd
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# 7. Запускаем и включаем автозапуск
sudo systemctl enable --now docker

# 8. Проверяем
docker --version
docker compose version

# 9. (очень рекомендуется) Добавить своего пользователя в группу docker
#    (чтобы не писать sudo каждый раз)
sudo usermod -aG docker $USER
# после этого нужно выйти и зайти
