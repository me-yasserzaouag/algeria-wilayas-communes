# Algeria - 69 Wilayas / 1541 Communes

Algérie · الجزائر - the **69 wilayas** (ولايات) and **1541 communes** (بلديات) of Algeria, with post codes, daïras (دوائر), Latin and Arabic names, and coordinates.

Division fixed by **loi n° 26-06 du 4 avril 2026**, published in the **Journal Officiel n° 25 du 5 avril 2026**:

> « Art. 3. - Le nouveau découpage territorial du pays comprend soixante-neuf (69) wilayas et mille cinq cent quarante-et-une (1541) communes. »

Each commune is attached to the wilaya the law gives it: the commune count of **every one of the 69 wilayas** matches the Journal Officiel.

JSON, CSV, XML, GeoJSON, and ready-to-run SQL for MySQL, PostgreSQL and SQL Server.

## Files

```
data/wilayas.json    data/wilayas.csv    data/wilayas.geojson    data/wilayas.xml       → 69 wilayas / ولايات
data/communes.json   data/communes.csv   data/communes.geojson   data/communes.xml   → 1541 communes / بلديات
sql/mysql.sql        sql/postgres.sql    sql/sqlserver.sql
tools/gen_sql.py           → regenerates sql/
```

GeoJSON follows RFC 7946: `Point` geometries, coordinates in `[longitude, latitude]` order, WGS 84.

CSV files are UTF-8 with BOM, so Arabic renders correctly in Excel.

## Schema

**wilaya** - `code` (1-69), `name`, `name_ar`, `latitude`, `longitude`

**commune** - `id` (1-1541), `post_code` (unique), `name`, `name_ar`, `daira`, `daira_ar`, `wilaya_code`, `latitude`, `longitude`

```json
{
  "id": 1,
  "post_code": "01001",
  "name": "Adrar",
  "name_ar": "أدرار",
  "daira": "Adrar",
  "daira_ar": "أدرار",
  "wilaya_code": 1,
  "latitude": 27.9763317,
  "longitude": -0.4841573
}
```

Coordinates are WGS 84. Suitable for map display and location pickers, not for routing or distance calculations.

`daira` and `daira_ar` are **nullable**: 1490 of the 1541 communes carry a daïra, 1432 of those confirmed by two independent sources. The remaining 51 are left null rather than guessed.

## Use `wilaya_code`, not the post code

For 70 communes the post-code prefix does not match the wilaya code - Boughezoul is post code `26051` and sits in wilaya 67. Post codes are postal identifiers and the 2026 reform did not renumber them.

## Sources

Legal reference: [JO n° 25 du 5 avril 2026](https://www.joradp.dz/FTP/jo-francais/2026/F2026025.pdf), loi n° 26-06 du 4 avril 2026, following the Council of Ministers of 16 November 2025.

## Rebuilding

```bash
python tools/gen_sql.py
```

Reads `data/*.json` and rewrites `sql/`.

## Commits

Use plain descriptive messages. The dataset changes only when the law changes, so the pattern is:

```
Update wilayas/communes for loi 26-XX
```

`sql/` is regenerated via `tools/gen_sql.py` and committed alongside the data it's derived from.

## Licence

MIT - see [LICENSE](LICENSE).
