# Custom Windows Server Image : Auto Installer

1. Download & Setup Installer :
Download file Installernya
- wget https://raw.githubusercontent.com/ownergpi/readme/main/windows-server-autoinstaller.sh

Beri permission ke file tersebut
- chmod +x windows-server-autoinstaller.sh

Jalankan installernya
- ./windows-server-autoinstaller.sh

2. Run QEMU :
Note - Ubah xxx sesuai dengan versi windows yang kalian pilih.

qemu-system-x86_64 \
-m 3G \
-cpu host \
-enable-kvm \
-boot order=d \
-drive file=windows2022.iso,media=cdrom \
-drive file=windows2022.img,format=raw,if=virtio \
-drive file=virtio-win.iso,media=cdrom \
-device usb-ehci,id=usb,bus=pci.0,addr=0x4 \
-device usb-tablet \
-vnc :0 \

PENTING : Enter 2x

4. Akses via VNC :
Buka RealVNC Viewer, masukkan IP VPS kalian. Setelah itu ikuti langkah langkah yang ada di video.

5. Download File Custom Windows Server Kalian :
Kompress Windows Server Img kalian
- dd if=windows2xxx.img | gzip -c>windows2xxx.gz

6. Install Apache
- apt install apache2

7. Beri akses firewall untuk Apache
- sudo ufw allow 'Apache'

9. Pindahkan file Windows Server Image kalian biar bisa di download
- cp windowsxxx.gz /var/www/html/
  
9. Buka browser, download dengan mengakses VPSnya. Ubah yyy dengan ip kalian, xxx untuk versi Windows Server yang kalian pilih
- http://yyy.yyy.yyy/windows2xxx.gz

10. Setting Agar Bisa Diakses via RDP :
Create droplet baru dan ikuti petunjuk yang ada di YouTube
- wget -O- --no-check-certificate http://yyy.yyy.yyy/windowsxxxx.gz | gunzip | dd of=/dev/vda
