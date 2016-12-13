## Oracle Secure Password Store (SEPS) ##

* prepare dir and sqlnet.ora, tnsnames.ora
  $ umask 0700
  $ mkdir $HOME/.wallet
  $ cd $HOME/.wallet
  $ cat > sqlnet.ora <<EOS;
  wallet_location = (source = (method = file) (method_data = (directory = $HOME/.wallet)))
  sqlnet.wallet_override = true
  EOS
  $ cat > tnsnames.ora <<EOS;
  c01 = (description = (address=(protocol=tcp)(port=1521)(host=127.0.0.1)) (connect_data=(sid=$ORACLE_SID)))
  EOS

* create wallet
  $ mkstore -wrl $HOME/.wallet -create

* add credential
  $ mkstore -wrl $HOME/.wallet -createCredential c01 zabbix

* list credential
  $ mkstore -wrl $HOME/.wallet -listCredential

* modify credential
  $ mkstore -wrl $HOME/.wallet -modifyCredential c01 zabbix
