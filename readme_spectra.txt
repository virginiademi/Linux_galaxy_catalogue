1. Nel directory pgn_files_spectra:
Devo ordinare gli spettri per nome corretto, sono 1262 alcuni mancano e per capire quali devo eseguire passaggio 3 in seguito.. intanto:
tentativi comandi

ls *png | awk -F .png '{print $1}' | awk -F spec_ '{print $2}' | head
ls *png | sed 's/spec/ /' | awk -F .png '{print $1}' | head
ls *png | awk -F _00 '{print $2}' | awk -F 0 '{print $2}' | head
trovato comando che crea lista spettri con i nomi giusti, ma non cambia nome ai files..
ls *png | awk -F spec '{print $2}' | sed 's/\_000/\_00/' | sed 's/\_00/\_0/' | sed 's/\_0/ /' | awk -F .png '{print $1}' > correct_name_spectra
serve un altro passaggio
awk '{print "mv spec_000" $1".png " $1"| mv spec_00" $1".png " $1 }' correct_name_spectra > ! command_test.com
chmod 777 command_test.com
./command_test.com
 FUNZIONA!
2. Nel directory fits_files_spectra:
Devo ordinare gli spettri per nome
ci sono 1288 spettri, devo filtrarne 1277 con nome capak:

ls *fits | awk -F sc '{print $2}' | sed 's/\_000/\_00/' | sed 's/\_00/\_0/' | sed 's/\_0/ /' | awk -F .fits '{print $1}' > correct_name_spectra_fits

awk '{print "mv sc_000" $1".fits " $1"| mv sc_00" $1".fits " $1 }' correct_name_spectra_fits > ! command_test.com
FUNZIONA!
3. Ora devo fare un confronto con gli id_capak:
cp correct_name_spectra_fits extra_spectra 
awk '{print $1}' extra_spectra > list_extra_spectra
per togliere lo spazio bianco davanti agli id..
awk '{ print "grep -v " $1 " list_extra_spectra \>! j \n \\mv j list_extra_spectra "} ' id_both.txt > ! comando.com
chmod 777 comando.com
./comando.com
LA MAGIC LINE: 
# ! usr/bin/csh
FUNZIONA 11 SPETTRI EXTRA!

4. Ora devo confrontare gli spettri fits e png per capire quali png mancano
1277 e' la lista degli spettri fits corretti nome capak
1262 e' la lista degli spettri png da controllare

awk '{ print "grep -v " $1 " 1277 \>! new_list \n \\mv new_list list " }' 1262 > ! v.com
wc list
1276
con diversi tentativi il risultato e' sempre questo.. 

forse esiste solo 1 png con nome capak.. provo a vedere se i 1262 hanno nome zcosmos
e' proprio cosi'!!!
cambio i nomi dei png in id_capak
awk '{ print "mv "$11" "$1 }' all_merged_including_finalz_flags > ! vi.com
cd ./png_files_spectra
chmod 777 vi.com
./vi.com
GLI SPETTRI PNG HANNO ORA NOME CAPAK TRANNE 13 CHE NON HANNO NOME NE' CAPAK NE' ZCOSMOS
questi 13 sono nel file ???
5. Ora riprovo il confronto 1277 1262 *(che ora e' 1262 -13)

awk '{ print "grep -v " $1 " 1277 \>! r \n \\mv r spettri_capak_mancanti " }' pgn_in_cpak > ! lk.com
LA MAGIC LINE: 
# ! usr/bin/csh


