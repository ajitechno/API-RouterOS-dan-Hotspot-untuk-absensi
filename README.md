# API-RouterOS-dan-Hotspot-untuk-absensi (versi ini sedang dalam tahap pengembangan)
Gateway Absensi adalah aplikasi yang bertujuan untuk merekap data kehadiran absensi mahasiswa/i. 
rekap data ini dibuat dengan menggunakan data dari Mikrotik RouterOS melalui layanan API, dan di kombinasikan dengan autentikasi hotspot sebagai data kehadiran mahasiswa/i.

Petunjuk penggunaan
1. set nama servers untuk mata kuliah 
2. set nama user profiles untuk kelas dan semester
scripts on login :
:local mac $"mac-address"; /ip hotspot user set mac-address=$mac [find where name=$user];
:local comment [ /ip hotspot user get [/ip hotspot user find where name="$user"] comment];
:local server [ /ip hotspot user get [/ip hotspot user find where name="$user"] server];
:local profile [ /ip hotspot user get [/ip hotspot user find where name="$user"] profile];
:local date [/system clock get date ];:local time [/system clock get time ];[/system script add name="$date-|-$time-|-$server-|-$profile-|-$user-|-$comment" owner="$server | $profile" source="$date | $time" comment="Absensi Gateway"];
:for j from=1 to=4 step=1 do={
   :for i from=2000 to=50 step=-400 do={
     :beep frequency=$i length=11ms;
     :delay 11ms;
   }
   :for i from=800 to=2000 step=400 do={
     :beep frequency=$i length=11ms;
     :delay 11ms;
   }
 };  
3. set user hotspot username = password dan comment untuk nama mahasiswa/i
4. login hotspot utk absensi
5. login ke aplikasi

Tested
Mikrotik RB951UI 2Hnd
Php 5, Bootstrap
terima kasih atas kontribusinya 
