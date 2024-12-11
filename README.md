# isletim-sistemleri-alistirma2
# Çoklu Programlama (Multithreading) Örnekleri
import time
import threading

def program1():
    for i in range(3):  # 3 defa çalışacak
        print(f"Program 1 çalışıyor: {i}")
        time.sleep(1)

def program2():
    for i in range(3):
        print(f"Program 2 çalışıyor: {i}")
        time.sleep(1)

def program3():
    for i in range(3):
        print(f"Program 3 çalışıyor: {i}")
        time.sleep(1)

if __name__ == "__main__":
    thread1 = threading.Thread(target=program1)
    thread2 = threading.Thread(target=program2)
    thread3 = threading.Thread(target=program3)

    thread1.start()
    thread2.start()
    thread3.start()

    thread1.join()
    thread2.join()
    thread3.join()

    print("Tüm programlar tamamlandı!")

# Çoklu İşlemci (Multiprocessing) Örnekleri
from multiprocessing import Process
import os

def hesapla(sayi):
    print(f"İşlemci: {os.getpid()} - Sayı: {sayi}, Kare: {sayi * sayi}")
    time.sleep(1)

if __name__ == "__main__":
    sayilar = [1, 2, 3, 4, 5, 6]
    islemler = []

    for sayi in sayilar:
        islem = Process(target=hesapla, args=(sayi,))
        islemler.append(islem)
        islem.start()

    for islem in islemler:
        islem.join()

    print("Tüm işlemler tamamlandı!")

# Thread ve Process Karşılaştırması Örnekleri

def thread_hesapla(sayi):
    print(f"Hesaplanıyor (Thread ID: {threading.get_ident()}): {sayi} -> {sayi * sayi}")
    time.sleep(1)

def process_hesapla(sayi):
    print(f"Hesaplanıyor (Process ID: {os.getpid()}): {sayi} -> {sayi * sayi}")
    time.sleep(1)

if __name__ == "__main__":
    sayilar = [10, 20, 30, 40]

    # Thread ile çoklu programlama
    print("\nÇoklu Programlama Başlıyor (Thread)...\n")
    threads = []
    for sayi in sayilar:
        t = threading.Thread(target=thread_hesapla, args=(sayi,))
        threads.append(t)
        t.start()

    for t in threads:
        t.join()

    print("\nÇoklu Programlama Tamamlandı (Thread)!")

    # Process ile çoklu işlemci
    print("\nÇoklu İşlemci Başlıyor (Process)...\n")
    processes = []
    for sayi in sayilar:
        p = Process(target=process_hesapla, args=(sayi,))
        processes.append(p)
        p.start()

    for p in processes:
        p.join()

    print("\nÇoklu İşlemci Tamamlandı (Process)!")
