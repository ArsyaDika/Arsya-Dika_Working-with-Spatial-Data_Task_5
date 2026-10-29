# Geoprocessing Poligon dengan GeoPandas

Rangkaian operasi geoprocessing dasar pada poligon kelas kerawanan di Bandung, dari data API MAPID hingga ekspor GeoJSON: reproject, buffer, simplify, clip, dissolve, union, hitung luas, dan filter atribut.

Tugas 5 bootcamp WebGIS Developer (Working with Spatial Data).

## Alur

| Langkah | Operasi | Output |
|---|---|---|
| 1 | Ambil poligon dari API MAPID, tampilkan di Folium | – |
| 2 | Set CRS EPSG:4326, reproject ke EPSG:3857 | – |
| 3 | Buffer 100 m | `buffered_layer_100meter_new.geojson` |
| 4 | Simplify (toleransi 5 m) | `Simplify_buffered_layer_100meter_new.geojson` |
| 5 | Clip ke bounding box area studi | `clipped_layer_new.geojson` |
| 6 | Dissolve per `KELAS` | `dissolved_layer_per_kelas_new.geojson` |
| 7 | Union seluruh poligon | `hasil_union_new.geojson` |
| 8 | Hitung luas (km²) di UTM 48S | `union_with_area_newest.geojson` |
| 9 | Filter `KELAS == "TINGGI"` | `filtered_tinggi_new.geojson` |

## Menjalankan

```bash
pip install geopandas folium requests
export MAPID_API_KEY=...        # PowerShell: $env:MAPID_API_KEY = "..."
jupyter notebook "Task day 5.ipynb"
```

API key dibaca dari environment variable, tidak lagi ditulis di notebook.

## Catatan perbaikan

- **API key dihapus** dari notebook. Key lama masih ada di riwayat commit, jadi sebaiknya dicabut di dashboard MAPID.
- **Buffer tidak tersimpan.** Hasil `buffer(100)` sebelumnya tidak di-assign, sehingga file "buffered" berisi poligon asli. Sudah diperbaiki.
- **Simplify tidak tersimpan.** Hasil `simplify` sebelumnya juga tidak dipakai, sehingga file "Simplify" sama dengan file buffer. Sudah diperbaiki, dengan toleransi dalam meter.
- **Luas salah satuan.** `AREA_KM2` sebelumnya dihitung di EPSG:4326 (derajat), sehingga nilainya sekitar 1e-10. Sekarang dihitung di UTM zona 48S (EPSG:32748).
- Clip sekarang memakai `gpd.clip`, dan path Windows absolut diganti path relatif.

Perbaikan sudah diuji pada data `filtered_tinggi_new.geojson`. **File GeoJSON di repo masih hasil versi lama.** Jalankan ulang notebook dengan API key untuk memperbaruinya.

## Tools

Python · GeoPandas · Shapely · Folium · MAPID API

## Penulis

**Arsya Dika** · [GitHub](https://github.com/ArsyaDika)
