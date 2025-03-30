# Ad-Filter 🚫✨

Списки доменов с рекламой на базе Hagezi Pro для использования с клиентами на базе Xray и Sing-Box. Ежедневное обновление.

## Особенности
- **Ежедневные обновления**: Автоматически загружает и обрабатывает последние списки [Hagezi Pro](https://github.com/hagezi/dns-blocklists) каждый день в полночь.
- **Два формата**:
  - `adlist.dat`: Список для Xray.
  - `adlist.srs`: Список для Sing-Box.
- **Простой доступ**: Статичные ссылки на последние файлы через GitHub Releases.

## Последние версии
Скачивайте самые свежие списки в любое время:

- 📦 [adlist.dat](https://github.com/zxc-rv/ad-filter/releases/latest/download/adlist.dat)  
- 📦 [adlist.srs](https://github.com/zxc-rv/ad-filter/releases/latest/download/adlist.srs)

## Как это работает
1. **Источник данных**: Загружаются домены из wildcard-списка Hagezi Pro.
2. **Обработка**: Удаляются комментарии, форматируются данные и компилируются в нужные форматы.
3. **Автоматизация**: GitHub Actions запускается ежедневно для создания и публикации файлов.
4. **Доставка**: Файлы публикуются как активы релиза GitHub для удобного доступа.

## Примеры конфигураций:

### Для Xray
Загрузите `adlist.dat` в нужную директорию и добавьте правило для него:

```json
{
  "routing": {
    "rules": [
      {
        "domain": "ext:adlist.dat:hagezi-pro",
        "outboundTag": "block"
      }
    ]
  }
}
```

### Для Sing-box
Добавьте rule_set в конфигурацию Sing-Box и правило для него:

```json
{
  "route": {
    "rules": [
      {
        "rule_set": "ads",
        "action": "reject"
      }
    ],
    "rule_set": [
      {
        "tag": "ads",
        "type": "remote",
        "format": "binary",
        "url": "https://github.com/zxc-rv/ad-filter/releases/latest/download/adlist.srs",
        "download_detour": "direct"
      }
    ]
  }
}
```


