## Primer script

* Como primer script se utilizará esearch -db nucleotide -query "Oxybelis[Organism] AND 16S[Title]" | efetch -format fasta > Oxybelis_16S.fasta este busca descargar todos los datos relacionados con el gen 16S en oxybelis
Se podría utilizar datasets con el comando ./datasets download gene symbol 16S taxon oxybelis --filename 16S_EmilioValdiviezo, sin embargo esto no sirve con genes ribosomales por lo cual se optará por el comando anterior

# Con el comando anterior ya tendríamos los archivos transformados a fasta, por lo que ahora es necesario alinearlo con muscle, para eso se ocupa el siguiente comando

* ./muscle3.8.31_i86linux64 -in Oxybelis_16S.fasta -out Oxybelis_16S.fasta.muscle -maxiters 1 -diags.


## Una vez alineado, se debe proceder con el programa Atom, el cual nos permitirá eliminar cualquier información no deseada para cada muestra como por ejemplo las siglas MT delante de cada especie

* En mi caso utilicé comandos como ^>.*? para eliminar información inecesaria.

# Siempre se debe añadir un grupo externo para complementar una filogenia, por lo cual es necesario entrar a NCBI y editar el archivo que generamos anteriormente añadiendo la información correspondiente

* si esto genera inconventientes en el archivo, al convertirlo en .txt se recomienda cambiar el nombre del mismo dentro de la plataforma de Hoffman 

## Luego se debe hacer uso de iqtree con el siguiente comando

* for filename in muscle_*
*  do
* iqtree2 -s $filename
* done


## También puede funcionar el comando
 
* iqtree2 -s Oxybelis_16S.fasta_EMILIO.muscle -nt AUTO -m MFP -bb 1000 -alrt 100

Cada una de las partes que componen el comando representan los siguiente

* -s: tu archivo de entrada alineado.

* -nt AUTO: usa múltiples núcleos automáticamente.

* -m MFP: IQ-TREE elige el mejor modelo evolutivo.

* -bb 1000: 1000 réplicas de bootstrap ultrarrápido.

* -alrt 1000: soporte SH-aLRT (test de rama).


#Luego el programa obtenido se debe abrir en FigTree para ver como quedaron las secuencias alineaas en el arbol final

* El programa queda como el PDF adjuntado a parte. 




