# Ubah dari node:18 ke node:20
FROM node:20-alpine

WORKDIR /app

# Salin package file
COPY package*.json ./

# Install ulang dependencies agar sesuai dengan environment Node baru
RUN npm install

# Salin sisa file
COPY . .

EXPOSE 5173

# Tambahkan --host agar bisa diakses dari luar container
CMD ["npm", "run", "dev", "--", "--host"]