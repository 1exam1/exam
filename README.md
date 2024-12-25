# exam
Вот подробная инструкция по клонированию репозитория с GitHub:

### 1. Установите Git
#### 1.1. Проверка установлен ли Git
Откройте терминал (или командную строку) и введите:  
```
git --version
```
Если Git установлен, вы увидите его версию (например, `git version 2.39.0`).  
Если нет, следуйте следующему шагу.

#### 1.2. Установка Git  
**Linux (Debian/Ubuntu):**  
```
sudo apt update
sudo apt install git
```
**MacOS (Homebrew):**  
```
brew install git
```
**Windows:**  
- Скачайте [Git для Windows](https://git-scm.com/download/win) и установите его, следуя инструкциям установщика.  

После установки снова выполните команду `git --version`, чтобы убедиться, что Git установлен.

---

### 2. Создайте папку для репозитория
В терминале перейдите в ту директорию, куда хотите склонировать репозиторий. Например:  
```
cd ~/projects
mkdir my_project
cd my_project
```

---

### 3. Найдите URL репозитория на GitHub
1. Перейдите на страницу репозитория, который хотите склонировать.  
2. Нажмите на зеленую кнопку `Code` (в правом верхнем углу).  
3. Выберите HTTPS и скопируйте URL (например, `https://github.com/user/repo.git`).  

---

### 4. Клонирование репозитория
Теперь выполните команду:  
```
git clone <URL_репозитория>
```
Пример:  
```
git clone https://github.com/user/repo.git
```

#### **Объяснение команды:**
- `git clone` — команда для клонирования репозитория.  
- `<URL_репозитория>` — адрес репозитория, который вы скопировали на GitHub.  

---

### 5. Переход в папку с клонированным репозиторием
После клонирования репозиторий будет находиться в новой папке с именем репозитория:  
```
cd repo
```

---

### 6. Проверка состояния репозитория
```
git status
```
Это покажет текущие изменения и статус репозитория.

---

### 7. Настройка привязки к удалённому репозиторию
Чтобы убедиться, что репозиторий правильно привязан к удалённому серверу, введите:  
```
git remote -v
```
Вы увидите что-то вроде:  
```
origin  https://github.com/user/repo.git (fetch)
origin  https://github.com/user/repo.git (push)
```

---

### 8. (Опционально) Установка SSH для GitHub (без постоянного ввода пароля)
1. **Проверьте, есть ли SSH-ключ:**  
```
ls ~/.ssh
```
Если ключей нет, создайте новый:  
```
ssh-keygen -t ed25519 -C "your_email@example.com"
```
Нажмите Enter, выберите место сохранения и установите пароль (по желанию).  
2. **Добавьте ключ в GitHub:**  
- Скопируйте ключ:  
```
cat ~/.ssh/id_ed25519.pub
```
- Зайдите в [настройки SSH на GitHub](https://github.com/settings/ssh) и добавьте новый SSH-ключ.  

Теперь вы можете использовать SSH для клонирования:  
```
git clone git@github.com:user/repo.git
```

---

### 9. Обновление локальной копии (Pull)
Если репозиторий обновился, вы можете получить изменения:  
```
git pull
```


## 🔑 Генерация SSH-ключа и привязка к GitHub

### 1. Генерация SSH-ключа

#### 1.1. Открой терминал и выполни команду:
```
ssh-keygen -t ed25519 -C "your_email@example.com"
```
- `-t ed25519` — более безопасный тип ключа (рекомендуется).  
- `-C "your_email@example.com"` — комментарий (лучше использовать email от GitHub).  

Если у тебя старая версия Git, используй RSA:
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
- `-b 4096` — длина ключа для RSA.

---

#### 1.2. Сохранение ключа
- После выполнения команды будет предложено выбрать путь для сохранения ключа.  
- Нажми `Enter`, чтобы сохранить в стандартную директорию (`~/.ssh/id_ed25519`).  

Пример:
```
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/user/.ssh/id_ed25519):
```

---

#### 1.3. Установка пароля для ключа (необязательно)
- Тебя попросят ввести пароль для защиты ключа.  
- Можешь оставить поле пустым и нажать `Enter`, если не хочешь ставить пароль.

```
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```

---

### 2. Добавление SSH-ключа в агент

Теперь добавим ключ в SSH-агент, чтобы он мог использоваться для аутентификации.

1. Убедись, что SSH-агент запущен:
```
eval "$(ssh-agent -s)"
```
Ответ будет примерно такой:
```
Agent pid 12345
```

2. Добавь ключ в агент:
```
ssh-add ~/.ssh/id_ed25519
```

---

### 3. Скопировать SSH-ключ

Скопируем публичную часть SSH-ключа, чтобы добавить его на GitHub:

```
cat ~/.ssh/id_ed25519.pub
```
- Копируй содержимое, начиная с `ssh-ed25519` и заканчивая email-адресом.

---

### 4. Добавление SSH-ключа на GitHub

1. Перейди в [настройки SSH и GPG ключей](https://github.com/settings/keys).  
2. Нажми кнопку **New SSH key**.  
3. В поле "Title" введи что-то вроде `My Laptop` или `Work PC`.  
4. Вставь скопированный ключ в поле "Key".  
5. Нажми **Add SSH key**.  

---

### 5. Проверка подключения

Теперь проверим, что ключ правильно работает:

```
ssh -T git@github.com
```
Если все в порядке, ты увидишь сообщение:
```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

Если появится предупреждение о fingerprint, введи `yes`.

---

### 6. Клонирование репозитория через SSH

Теперь можешь клонировать репозиторий с помощью SSH:

```
git clone git@github.com:user/repo.git
