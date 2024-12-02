# Как эта страничка сделана


## Настройка ssh ключей github
- Генерим ключ и копируем его публичную часть
```
cd ~
ssh-keygen -t ed25519
cat .ssh/id_ed25519.pub
```
- Новый ssh ключ добавляем сюда https://github.com/settings/keys

## Создание репозитория
- Создаем новый репозиторий по инструкции для User or Organization (https://pages.github.com/)
```
git clone git@github.com:bobkinstreet/bobkinstreet.github.io.git
cd bobkinstret.github.io/
```
- Создаем index.html, коммитим изменения
```
echo "Ученье свет" > index.html
git add .
git commit -m 'initial'
git push -u origin main
```
- После этого по адресу bobkinstreet.github.io будет доступен index.html. У меня страничка стала доступная только после второго коммита.

## Установка mkdocs
Устанавливаем mkdocs и тему
```
pip install mkdocs
pip install mkdocs-terminal
```

## Создаем и первично настраиваем странички

- Создаем mkdocs папку исходниками проекта прямо в репозитории в ветке main
```
mkdocs new src
```

- Первично кастомизируем [mkdocs.yml](https://raw.githubusercontent.com/bobkinstreet/bobkinstreet.github.io/refs/heads/main/src/mkdocs.yml)
```
site_name: Бобкин стрит
theme:
  name: terminal
  palette: pink
nav:
  - Домашняя: index.md
  - Об: about.md
markdown_extensions:
  - def_lists
# ...
```

- Проверяем как выглядит
```
mkdocs serve --config-file ./src/mkdocs.yml
```

## Кастомизирем базовый html
==не_работает==

- Создаем main.html https://www.mkdocs.org/user-guide/customizing-your-theme/#overriding-template-blocks
```
mkdir src/custom_dir
touch src/custom_dir/footer.html
```

- И наполням его
```
{% extends "base.html" %}

{% block footer %}
Кастом текст
{% endblock %}
```
## Деплоимся
```
git checkout -b gh-pages
git push origin gh-pages
git checkout main

mkdocs gh-deploy --config-file ./src/mkdocs.yml --remote-branch gh-pages
```
