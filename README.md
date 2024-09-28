# Dokumantasi Pembayaran Pajak Daerah Kab. Gunungkidul
### Apa itu host to host Pembayaran?
Adalah layanan pengiriman instruksi pemindahan dana/pembayaran yang terintegrasi langsung dari sistem data tagihan pajak daerah ke Bank/Tempat Pembayaran.

### Siapa yang sudah bekerja sama?
Pada saat ini yang sudah bekerjasama dengan Pemerintah Kab. Gunungkidul adalah:
* [Bank BPD DIY](https://bpddiy.co.id)
* [Kantor POS](https://www.posindonesia.co.id/)
* [Bank BNI](https://www.bni.co.id/)

## Dokumentasi Teknis
### Inquiry (mengambil data tagihan)

```
{{base_url}}/pajak_daerah/getesptpd/{{auth_id}}/?user = {{user}}&idbilling = {{idbilling}}
```

Akan menghasilkan respon (respon berbentuk JSON)
* auth_id salah

  
```json
{
    "status": "1",
    "pesan": "Kode Keamanan salah"
}
```

* Tagihan sudah terbayar

  
```json
{
    "status": "2",
    "pesan": "Tagihan sudah terbayar"
}
```

* Tagihan terbayar dengan kelebihan pembayaran

  
```json
{
    "status": "2",
    "pesan": "Tagihan sudah terbayar dengan kelebihan pembayaran"
}
```

* Tagihan tidak ditemukan

  
```json
{
    "status": "1",
    "pesan": "Data tidak ditemukan"
}
```


* Id Billing Belum terbayar

```JSON
{
    "status": "0",
    "pesan": "Sukses",
    "data": [
        {
            "{{ data tagihan }}"
        }
    ]
}
```

### POSTED (melunaskan data tagihan)

```
{{base_url}}/pajak_daerah/postesptpd/{{auth_id}}/
```
Menggunakan method pos dan input JSON

```json
{
    "user":"{{ username }}",
    "IDBILLING":"{{ idbilling }}",
    "NORESI":"{{ noresi }}",
    "PEMBAYARAN":"{{ Total Pembayaran (pokok + denda) }}"
}
```
akan menghasilkan output sebagai berikut ini

* auth_id Salah
  
```json
{
    "status": "1",
    "pesan": "Kode Keamanan salah"
}
```

* Pembayaran Kurang
  
```json
{
    "status": "1",
    "pesan": "Pembayaran kurang"
}
```

* Pembayaran berhasil
```json
{
    "status": "0",
    "pesan": "Pembayaran Sukses",
}
```
