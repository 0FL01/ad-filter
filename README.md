# Ad-Filter 🚫✨

Списки рекламных доменов на базе Hagezi-pro для использования с клиентами на базе Xray и Sing-Box. Обновляется ежедневно.

## Особенности
- **Ежедневные обновления**: Автоматически загружает и обрабатывает последние [домены Hagezi Pro](https://github.com/hagezi/dns-blocklists) каждый день в полночь по UTC.
- **Два формата**:
  - `adlist.dat`: Список для Xray.
  - `adlist.srs`: Список для Sing-Box.
- **Простой доступ**: Статичные ссылки на последние файлы через GitHub Releases.

## Последние версии
Скачивайте самые свежие списки в любое время:

- 📦 [adlist.dat](https://github.com/zxc-rv/ad-filter/releases/latest/download/adlist.dat)  
- 📦 [adlist.srs](https://github.com/zxc-rv/ad-filter/releases/latest/download/adlist.srs)

## Как это работает
1. **Источник данных**: Загружает домены из wildcard-списка Hagezi.
2. **Обработка**: Удаляет комментарии, форматирует данные и компилирует в нужные форматы.
3. **Автоматизация**: GitHub Actions запускается ежедневно для создания и публикации файлов.
4. **Доставка**: Файлы публикуются как активы релиза GitHub для удобного доступа.

## Использование

### Для Xray
Используйте `adlist.dat` в конфигурации Xray для блокировки через список доменов:

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
Используйте `adlist.srs` в конфигурации Sing-box для блокировки рекламы:

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



- Скачайте `adlist.dat` и поместите его рядом с конфигурацией Xray.
- Убедитесь, что секция `hagezi-pro` соответствует формату файла.


