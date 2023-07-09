# Wilayah-Indonesia
Wilayah indonesia
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
