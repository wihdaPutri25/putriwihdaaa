# Rental API dengan NestJS, Prisma, dan GraphQL

API untuk sistem penyewaan kendaraan yang dibangun dengan NestJS, Prisma ORM, SQLite, dan GraphQL.

## Fitur
- CRUD penyewaan via REST API
- Query dan mutation via GraphQL
- Data pelanggan, kendaraan, dan penyewaan
- Seeder awal data dengan NIM 018
- Alias route `/apollo` untuk membuka Apollo Sandbox

## Struktur utama
- `src/main.ts` — bootstrap aplikasi dan seeding data awal
- `src/app.module.ts` — konfigurasi modul utama dan GraphQL
- `src/penyewaan/` — controller, service, resolver, DTO, model
- `prisma/schema.prisma` — model database

## Jalankan aplikasi
```bash
npm install
npm run build
npm start
```

Aplikasi akan berjalan di:
- http://localhost:3000/
- http://localhost:3000/apollo
- http://localhost:3000/graphql

## Endpoint REST
### GET /
Mengembalikan informasi endpoint utama.

### GET /penyewaan
Menampilkan semua data penyewaan beserta relasi pelanggan dan kendaraan.

### GET /penyewaan/:id
Menampilkan satu data penyewaan berdasarkan ID.

### POST /penyewaan
Membuat data penyewaan baru dengan body JSON:

```json
{
  "pelangganId": 1,
  "kendaraanId": 1,
  "totalBiaya": 1500000,
  "tanggalSewa": "2026-11-07T08:00:00.000Z"
}
```

### DELETE /penyewaan/:id
Menghapus data penyewaan berdasarkan ID.

## Query GraphQL
```graphql
query {
  penyewaanList {
    id
    totalBiaya
    tanggalSewa
    pelanggan {
      id
      nim
      nama
    }
    kendaraan {
      id
      merek
      model
      nomorPlat
    }
  }
}
```

```graphql
query {
  penyewaan(id: 1) {
    id
    totalBiaya
    pelanggan {
      nama
    }
  }
}
```

## Mutation GraphQL
### createPenyewaan
```graphql
mutation {
  createPenyewaan(input: {
    pelangganId: 1
    kendaraanId: 1
    totalBiaya: 1800000
    tanggalSewa: "2026-11-07T08:00:00.000Z"
  }) {
    id
    totalBiaya
    pelanggan {
      nama
    }
    kendaraan {
      model
    }
  }
}
```

### updatePenyewaan
```graphql
mutation {
  updatePenyewaan(input: {
    id: 1
    totalBiaya: 2200000
  }) {
    id
    totalBiaya
  }
}
```

### deletePenyewaan
```graphql
mutation {
  deletePenyewaan(id: 1) {
    id
  }
}
```

## Data awal
Data pelanggan awal yang dibangkitkan otomatis:
- NIM: 018
- Nama: Mahasiswa 018
- Email: 018@example.com

## Catatan
- Port aplikasi default: 3000
- Jika port sudah terpakai, hentikan proses lama lalu jalankan ulang `npm start`
- `/apollo` akan redirect ke GraphQL UI, sedangkan endpoint utama GraphQL tetap di `/graphql`
