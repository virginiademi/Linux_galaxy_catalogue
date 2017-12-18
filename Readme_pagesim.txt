Obiettivo: creare una pagina html per ogni immagine ..
Ogni pagina sara’ chiamata #numcapak_images.html

1- creo Template pagina: Image.html

2- per cambiare il titolo e creare 1277 pagine diverse:
awk '{print " sed \"s/xxxxxxx\/" $1 "_images.html\" Image.html" }' all_merged_including_finalz_flags>command_file

3- copio e incollo in command_file nel terminal per far correre i comandi


tutto cio’ non sta funzionando..
SOLUZIONE TROVATA:

il command sed corretto e’: awk '{print "sed \"s/xxxxxxx/" $1 "/\" Image.html \>!" $1 "_images.html"}' id_capak.txt >! sed_command.com

il risultato sara’ la creazione di una pagina web per ogni galassia dove appaia la scritta “images of galaxy #numcapak”
chmod 777 sed_command.com  
./sed_command.com 
 RIUSCITO! pagine inserite in cartella Images_pages
 4. voglio cambiare un pezzo da images of galaxy a solo galaxy 
sed -i "s/IMAGES OF/ /" *_images.html

