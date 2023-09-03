# ci-cd-demo
1) github.com
2) Регистрация
3) Переходим по ссылке https://github.com/t-chyngyz/ci-cd-demo2
4) Делаем форк проекта ('Create a new fork')
5) Жмем кнопку ('Add file' / 'Create new file')
6) В поле 'Name your file' пишем (.github/workflows/ci-cd-demo.yml)
7) В контент вводим:
``` yaml
name: GitHub Actions Demo
on:
  push:
    branches: [ master, main ]
  pull_request:
    branches: [ master, main ]
jobs:
  init:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-varsion: [ 17.x ]
    steps:
      - uses: actions/checkout@v3
      - name: Staring Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node-version }}
      - name: install modules
        run: npm install
      - name: build project
        run: npm run build
      - name: build storybook
        run: npm run build:storybook
      - name: unit test
        run: npm run test:unit
      - name: e2e test
        run: npm run test:e2e
      - name: lint code
        run: npm run lint
```
