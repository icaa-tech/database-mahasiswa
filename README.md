# database-mahasiswa
import tkinter as tk
from tkinter import messagebox

# Data disimpan dalam list
data_mahasiswa = []

# Fungsi Tambah
def tambah_data():
    id_mhs = entry_id.get()
    nama = entry_nama.get()
    nim = entry_nim.get()
    if id_mhs and nama and nim:
        # Cek apakah ID sudah ada
        for mhs in data_mahasiswa:
            if mhs['id'] == id_mhs:
                messagebox.showwarning("Peringatan", "ID sudah digunakan")
                return
        data_mahasiswa.append({'id': id_mhs, 'nama': nama, 'nim': nim})
        tampilkan_data()
        entry_id.delete(0, tk.END)
        entry_nama.delete(0, tk.END)
        entry_nim.delete(0, tk.END)
    else:
        messagebox.showwarning("Peringatan", "Semua field harus diisi")

# Fungsi Update
def update_data():
    id_mhs = entry_id.get()
    nama = entry_nama.get()
    nim = entry_nim.get()
    for mhs in data_mahasiswa:
        if mhs['id'] == id_mhs:
            mhs['nama'] = nama
            mhs['nim'] = nim
            tampilkan_data()
            return
    messagebox.showwarning("Peringatan", "Data dengan ID tersebut tidak ditemukan")

# Fungsi Hapus
def hapus_data():
    id_mhs = entry_id.get()
    for mhs in data_mahasiswa:
        if mhs['id'] == id_mhs:
            data_mahasiswa.remove(mhs)
            tampilkan_data()
            return
    messagebox.showwarning("Peringatan", "Data dengan ID tersebut tidak ditemukan")

# Tampilkan data ke listbox
def tampilkan_data():
    listbox.delete(0, tk.END)
    for mhs in data_mahasiswa:
        listbox.insert(tk.END, f"{mhs['id']} - {mhs['nama']} ({mhs['nim']})")

# Buat jendela GUI
root = tk.Tk()
root.title("Data Mahasiswa")

# Label dan Entry
tk.Label(root, text="ID").grid(row=0, column=0, padx=5, pady=5)
entry_id = tk.Entry(root)
entry_id.grid(row=0, column=1, padx=5, pady=5)

tk.Label(root, text="Nama").grid(row=1, column=0, padx=5, pady=5)
entry_nama = tk.Entry(root)
entry_nama.grid(row=1, column=1, padx=5, pady=5)

tk.Label(root, text="NIM").grid(row=2, column=0, padx=5, pady=5)
entry_nim = tk.Entry(root)
entry_nim.grid(row=2, column=1, padx=5, pady=5)

# Tombol
tk.Button(root, text="Tambah", command=tambah_data).grid(row=3, column=0, padx=5, pady=5)
tk.Button(root, text="Update", command=update_data).grid(row=3, column=1, padx=5, pady=5)
tk.Button(root, text="Hapus", command=hapus_data).grid(row=4, column=0, columnspan=2, padx=5, pady=5)

# Listbox untuk menampilkan data
listbox = tk.Listbox(root, width=50)
listbox.grid(row=5, column=0, columnspan=2, padx=5, pady=10)

# Jalankan GUI
root.mainloop()
