//bitbiket git init git remote add origin ssh://git@bitbucket.org/ServerPrimate/repository-name.git git remote add origin git@bitbucket.org:primatehiberica/paymeter.git

git add . git commit -m "First commit" git push -f origin master

Crear un script en el webroot

<-


Specify the files to be backed up.


Below command will backup everything inside the project folder

git add .


Committing to the local repository with a message containing the time details

curtime=date git commit -m "Automatic Backup @ $curtime"


Push the local snapshot to a remote destination

git push origin master

->

descargar repo

git clone https://xxxxx@bitbucket.org/xxxx/xxxxx.git

añadir permisos de ejecución chmod +x git.run añadir en /root/scripts/BitBucket.sh git pull origin master //Docu: //http://sivareddy.in/automatic-backup-project-data-git //http://rogerdudler.github.io/git-guide/

32 git remote add origin https://PabloPrimate@bitbucket.org/primatehiberica/gofer.git 33 git push -u origin --all 34 git push -u origin --all 35 git push -u origin --all 38 git init 39 git add . 40 git commit -m "initial commit of full repository" 41 git remote add origin https://PabloPrimate@bitbucket.org/primatehiberica/moncake.git 42 git push -u origin --all 47 git init 48 git add . 49 git commit -m "initial commit of full repository" 50 git remote add origin https://PabloPrimate@bitbucket.org/primatehiberica/payments-bridge.git 51 git push -u origin master 54 git init 55 git add . 56 git commit -m "initial commit of full repository" 57 git remote add origin https://PabloPrimate@bitbucket.org/primatehiberica/payments-bridge.git 58 git push -u origin master 60 git init 61 git add . 62 git commit -m "initial commit of full repository" 63 git remote add origin https://PabloPrimate@bitbucket.org/primatehiberica/apache.git 64 git push -u origin master 78 cd .git/ 91 nano git.run 93 cd .git/ 101 nano .git/config 104 cd .git/

111 chmod +x ./git.run 113 nano ./git.run 115 nano git 116 nano .git 117 nano .git/config 118 nano .git/config 124 nano .git/config 125 chmod +x ./git.run 128 chmod +x ./git.run 129 nano .git/config 133 nano .git/config 138 nano .git/config 142 nano .git/config 144 nano .git/config 151 chmod +x git.run 158 git clone https://shuntr@bitbucket.org/primatehiberica/gofer.git 215 git clone https://shuntr@bitbucket.org/primatehiberica/gofer.git 216 git clone https://shuntr@bitbucket.org/primatehiberica/gofer.git 217 git clone https://shuntr@bitbucket.org/primatehiberica/gofer.git 218 git clone https://shuntr@bitbucket.org/primatehiberica/gofer.git 390 history | grep git 399 git clone https://shuntr@bitbucket.org/primatehiberica/gofer.git 415 history | grep git 419 git clone https://shuntr@bitbucket.org/primatehiberica/moncake.git 463 git pull 464 git pull 465 git fetch origin 466 git pull 467 git status 468 git checkout all 469 git checkout 470 git checkout config/app-php 471 git checkout config/app.php 472 git checkout logs/debug.log 473 git checkout src/Controller/CashMovementsController.php 474 git checkout src/Controller/ExpensesController.php 475 git checkout src/Controller/FundsController.php 476 git checkout src/Controller/RentalsController.php 477 git checkout src/Locale/es/default.mo 478 git checkout src/Locale/es/default.po 479 git checkout src/Template/CashMovements/index.ctp 480 git checkout tmp/cache/models/myapp_cake_model_debug_kit_panels 481 git checkout tmp/cache/models/myapp_cake_model_debug_kit_requests 482 git checkout tmp/cache/models/myapp_cake_model_default_apartments 483 git checkout tmp/cache/models/myapp_cake_model_default_configuration 484 git checkout tmp/cache/models/myapp_cake_model_default_contracts_owner 485 git checkout tmp/cache/models/myapp_cake_model_default_languages 486 git checkout tmp/cache/models/myapp_cake_model_default_users 487 git checkout tmp/cache/models/myapp_cake_model_default_web_texts 488 git checkout tmp/cache/models/myapp_cake_model_default_web_texts_i18n 489 git checkout tmp/cache/persistent/myapp_cake_core_translations_cake_es 490 git checkout tmp/cache/persistent/myapp_cake_core_translations_debug_kit_enu_s 491 git checkout 492 git checkout src/Template/CashMovements/index.ct 493 git checkout tmp/cache/persistent/myapp_cake_core_translations_default_es 494 git checkout tmp/cache/persistent/myapp_cake_core_translations_default_enu_s 495 git checkout tmp/cache/persistent/myapp_cake_core_translations_debug_kit_es 496 git checkout logs/error.log 497 git pull 498 git pull 499 git pull 500 git pull

git checkout -- *