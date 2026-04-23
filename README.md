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
sud
