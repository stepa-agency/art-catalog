# Art Catalog

Каталог картин с выставки, доступных для покупки.

- [`catalog.json`](catalog.json) — структурированный список картин (техника, цена, описание, ссылки на фото)
- [`photos/`](photos) — фотографии картин

## Формат записи в catalog.json

```json
{
  "id": "001",
  "title": null,
  "technique": "",
  "price": null,
  "currency": "",
  "description": "",
  "photos": ["photos/001_1.jpg"],
  "added_at": "YYYY-MM-DD"
}
```
