## Création de Keepass 

1- Création des Keepasspour de la prod les BUs  : 
2- Création des Keepass de la Preprod pour les Bus : 
Connecter au KeePass 
Click droit duplicate entry : title, name Generate clet name 

###########################
### Création de Keytab  ###
###########################

kinit svc_hdp-p_u_pprod_002_stb@INT.ADEO.COM
ktutil 
addent -password -p svc_hdp-p_u_pprod_002_stb@INT.ADEO.COM  -k 0 -e arcfour-hmac
wkt svc_hdp-p_u_pprod_001_stb.keytab
q

pour vérifier que le keytab est créer il faut lancer la commande :
klist -kte svc_hdp-p_u_pprod_004_stb.keytab

pour vérifier que le Keytab est créer il faut lance la commande :
klist -kte svc_hdp-p_u_pprod_004_stb.keytab

Pour vérifier si les groupe sont créer il faut lancer la commande :
id svc_hdp-p_u_pprod_015_stb

Pour vérifier que les keytab ils sont bien créer il faut lancer le script:

while read keytab; do echo '##'; echo $keytab; echo '##'; klist -kte $keytab; kinit $( awk -F'.' '{print $1}' <<< $keytab  ) -kt $keytab; 
id $( awk -F'.' '{print $1}' <<< $keytab  ); done< <( ls *.keytab ))

