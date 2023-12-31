# Wilayah-Indonesia
Wilayah indonesia
untuk data wilayah dari repo berikut : [Repo](https://github.com/cahyadsn/wilayah.git).
## Split menjadi 4 table

```
CREATE TABLE master_provinsi (
  id VARCHAR (36),
  kode VARCHAR (50) NOT NULL,
  nama VARCHAR (255) NOT NULL,
  PRIMARY KEY (id),
  UNIQUE (kode)
);

CREATE TABLE master_kota_kabupaten (
  id VARCHAR (36),
  master_provinsi_id VARCHAR (36) NOT NULL,
  kode VARCHAR (50) NOT NULL,
  nama VARCHAR (255) NOT NULL,
  PRIMARY KEY (id),
  UNIQUE (kode),
  FOREIGN KEY (master_provinsi_id) REFERENCES master_provinsi (id)
);

CREATE TABLE master_kecamatan (
  id VARCHAR (36),
  master_kota_kabupaten_id VARCHAR (36) NOT NULL,
  kode VARCHAR (50) NOT NULL,
  nama VARCHAR (255) NOT NULL,
  PRIMARY KEY (id),
  UNIQUE (kode),
  FOREIGN KEY (master_kota_kabupaten_id) REFERENCES master_kota_kabupaten (id)
);

CREATE TABLE master_kelurahan (
  id VARCHAR (36),
  master_kecamatan_id VARCHAR (36) NOT NULL,
  kode VARCHAR (50) NOT NULL,
  nama VARCHAR (255) NOT NULL,
  PRIMARY KEY (id),
  UNIQUE (kode),
  FOREIGN KEY (master_kecamatan_id) REFERENCES master_kecamatan (id)
);


```

## Migration ke 4 Table

```
INSERT INTO master_provinsi (id, kode, nama)
SELECT kode AS id, kode, nama FROM wilayah WHERE LENGTH(kode) = 2;

INSERT INTO master_kota_kabupaten (id, master_provinsi_id, kode, nama)
SELECT kode AS id, SUBSTRING(kode, 1, 2) AS master_provinsi_id, kode, nama FROM wilayah WHERE LENGTH(kode) = 5;

INSERT INTO master_kecamatan (id, master_kota_kabupaten_id, kode, nama)
SELECT kode AS id, SUBSTRING(kode, 1, 5) AS master_kota_kabupaten_id, kode, nama FROM wilayah WHERE LENGTH(kode) = 8;

INSERT INTO master_kelurahan (id, master_kecamatan_id, kode, nama)
SELECT kode AS id, SUBSTRING(kode, 1, 8) AS master_kecamatan_id, kode, nama FROM wilayah WHERE LENGTH(kode) = 13;
```
