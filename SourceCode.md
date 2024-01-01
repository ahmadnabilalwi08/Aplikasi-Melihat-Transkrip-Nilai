public class MataKuliah {
    private String kode;
    private String nama;
    private int sks;

    public MataKuliah(String kode, String nama, int sks) {
        this.kode = kode;
        this.nama = nama;
        this.sks = sks;
    }

    public String getKode() {
        return kode;
    }

    public String getNama() {
        return nama;
    }

    public int getSks() {
        return sks;
    }
}

public class TranskripAkademik {
    private String semester;
    private MataKuliah mataKuliah;
    private String nilai;

    public TranskripAkademik(String semester, MataKuliah mataKuliah, String nilai) {
        this.semester = semester;
        this.mataKuliah = mataKuliah;
        this.nilai = nilai;
    }

    public String getSemester() {
        return semester;
    }

    public MataKuliah getMataKuliah() {
        return mataKuliah;
    }

    public String getNilai() {
        return nilai;
    }
}

import java.util.ArrayList;

public class Mahasiswa {
    private String nim;
    private String nama;
    private ArrayList<TranskripAkademik> transkripList;

    public Mahasiswa(String nim, String nama) {
        this.nim = nim;
        this.nama = nama;
        this.transkripList = new ArrayList<>();
    }

    public String getNim() {
        return nim;
    }

    public String getNama() {
        return nama;
    }

    public ArrayList<TranskripAkademik> getTranskripList() {
        return transkripList;
    }

    public void tambahTranskrip(TranskripAkademik transkrip) {
        transkripList.add(transkrip);
    }
}

import java.util.Scanner;

public class TranskripViewer {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        try {
            // Input NIM
            System.out.print("Masukkan NIM: ");
            String nim = scanner.nextLine();

            // Input Nama
            System.out.print("Masukkan Nama: ");
            String nama = scanner.nextLine();

            // Membuat objek Mahasiswa
            Mahasiswa mahasiswa = new Mahasiswa(nim, nama);

            // Menambahkan transkrip Semester Gasal 2022
            mahasiswa.tambahTranskrip(new TranskripAkademik("Semester Gasal 2022", new MataKuliah("211810120", "Al Quran dan Hadits", 2), "A"));
            mahasiswa.tambahTranskrip(new TranskripAkademik("Semester Gasal 2022", new MataKuliah("211810811", "Praktikum Dasar Pemrograman", 1), "B"));
            mahasiswa.tambahTranskrip(new TranskripAkademik("Semester Gasal 2022", new MataKuliah("211810720", "Pancasila", 2), "A"));
            mahasiswa.tambahTranskrip(new TranskripAkademik("Semester Gasal 2022", new MataKuliah("211810630", "Manajemen Data dan Informasi", 3), "B+"));
            mahasiswa.tambahTranskrip(new TranskripAkademik("Semester Gasal 2022", new MataKuliah("211810531", "Logika Informatika", 3), "B+"));

            // Menambahkan transkrip Semester Genap 2022
            mahasiswa.tambahTranskrip(new TranskripAkademik("Semester Genap 2022", new MataKuliah("211820820", "Pendidikan Kewarganegaraan", 2), "A-"));
            mahasiswa.tambahTranskrip(new TranskripAkademik("Semester Genap 2022", new MataKuliah("211820731", "Pemrograman Web", 3), "A-"));
            mahasiswa.tambahTranskrip(new TranskripAkademik("Semester Genap 2022", new MataKuliah("211820520", "Bahasa Indonesia", 2), "A"));
            mahasiswa.tambahTranskrip(new TranskripAkademik("Semester Genap 2022", new MataKuliah("211820430", "Arsitektur Komputer", 3), "B+"));

            // Menambahkan transkrip Semester Ujian Ulang/Perbaikan Gasal 2022
            mahasiswa.tambahTranskrip(new TranskripAkademik("Semester Ujian Ulang/Perbaikan Gasal 2022", new MataKuliah("211810431", "Kalkulus Informatika", 3), "C+"));

            // Menambahkan transkrip Semester Ujian Ulang/Perbaikan Genap 2022
            mahasiswa.tambahTranskrip(new TranskripAkademik("Semester Ujian Ulang/Perbaikan Genap 2022", new MataKuliah("211820631", "Matematika Diskrit", 3), "B"));

            // Menampilkan transkrip
            System.out.println("Transkrip Akademik " + mahasiswa.getNama() + " (NIM: " + mahasiswa.getNim() + ")");
            System.out.println("--------------------------------------------------------");
            System.out.println("Pilih Semester yang ingin ditampilkan:");
            System.out.println("1. Semester Gasal 2022");
            System.out.println("2. Semester Genap 2022");
            System.out.println("3. Semester Ujian Ulang/Perbaikan Gasal 2022");
            System.out.println("4. Semester Ujian Ulang/Perbaikan Genap 2022");
            System.out.print("Masukkan pilihan (1-4): ");

            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume the newline character

            switch (choice) {
                case 1:
                    displayTranskrip(mahasiswa, "Semester Gasal 2022");
                    break;
                case 2:
                    displayTranskrip(mahasiswa, "Semester Genap 2022");
                    break;
                case 3:
                    displayTranskrip(mahasiswa, "Semester Ujian Ulang/Perbaikan Gasal 2022");
                    break;
                case 4:
                    displayTranskrip(mahasiswa, "Semester Ujian Ulang/Perbaikan Genap 2022");
                    break;
                default:
                    System.out.println("Pilihan tidak valid");
            }
        } catch (Exception e) {
            System.out.println("Terjadi kesalahan: " + e.getMessage());
            e.printStackTrace();
        } finally {

            if (scanner != null) {
                scanner.close();
            }
        }
    }

    private static void displayTranskrip(Mahasiswa mahasiswa, String semester) {
        System.out.println("----------------------------------------------------------------------------------------");
        System.out.printf("%-20s%-50s%-10s%-5s%n", "Semester", "Mata Kuliah", "SKS", "Nilai");
        System.out.println("----------------------------------------------------------------------------------------");
        for (TranskripAkademik transkrip : mahasiswa.getTranskripList()) {
            if (transkrip.getSemester().equals(semester)) {
                MataKuliah mataKuliah = transkrip.getMataKuliah();
                System.out.printf("%-20s%-50s%-10d%-5s%n", transkrip.getSemester(), mataKuliah.getNama(), mataKuliah.getSks(), transkrip.getNilai());
            }
        }
    }
}
