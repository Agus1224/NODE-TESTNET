# Challenge 6 StakeWars

# Membuat Ping Otomatis Setiap 5 Menit
Pada bagian ini kalian akan membuat transaksi otomatis untuk melakukan ping pada validators kalian.

1. Buat Folder Untuk Log

    ```bash
    mkdir $HOME/nearcore/logs
    ```
  
2. Buat file ping.sh
  
    ```
    nano $HOME/nearcore/scripts/ping.sh
    ```
  
3. Lalu isi filenya dengan kode dibawah ini

    ganti `xx` dengan nama wallet kalian (contoh : tester01) tanpa `.shardnet.near` atau `.factory.shardnet.near`.

    ```bash
    #!/bin/sh
    # Ping call to renew Proposal added to crontab

    export NEAR_ENV=shardnet
    export LOGS=$HOME/nearcore/logs
    export POOLID="xx"
    export ACCOUNTID="xx"

    echo "---" >> $LOGS/all.log
    date >> $LOGS/all.log
    near call $POOLID.factory.shardnet.near ping '{}' --accountId $ACCOUNTID.shardnet.near --gas=300000000000000 >> $LOGS/all.log
    near proposals | grep $POOLID >> $LOGS/all.log
    near validators current | grep $POOLID >> $LOGS/all.log
    near validators next | grep $POOLID >> $LOGS/all.log
    ```
4. Lalu buka crontab
    
    ```bash
    crontab -e
    ```

5. Lalu pilih nomor 1 untuk mengedit file dengan `nano`


6. Masukkan kode dibawah ini

    ```bash
    */5 * * * * sh $HOME/nearcore/scripts/ping.sh
    ```
    
    Lalu tekan `CTRL + O` dan `CTRL + X`.
    
7. Cek Log
  
    ```bash
    cat $HOME/nearcore/logs/all.log
    ```

