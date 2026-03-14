# Configure the firmware PIB files

Before you can flash the firmware, you need to configure a Unique PIB file for each powerline adapter so it contains all the settings and keys you want each powerline adapter to use. See the previous two steps for more details on the individual switches/flags.

Each PIB file must have the MAC ID and DAK unique to the powerline adapter for it to work properly. You can change the MAC ID and DAK using the Force Flash (-FF) switch/flag but it must be unique to each powerline adapter.


### Shared settings

```
.\hpavkey -e -M "Unique NMK Shared amongst all the 3 adapters!"
0EEA122814161DC997AEB1F277A39DC1
.\modpib -L1 -S "[MFG]" -T "[NET]" -U "[USR]" -N 0EEA122814161DC997AEB1F277A39DC1 "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\Hub.pib"
.\modpib -L1 -S "[MFG]" -T "[NET]" -U "[USR]" -N 0EEA122814161DC997AEB1F277A39DC1 "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\PA2.pib"
.\modpib -L1 -S "[MFG]" -T "[NET]" -U "[USR]" -N 0EEA122814161DC997AEB1F277A39DC1 "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\PA3.pib"
```

### Unique Hub Powerline Adapter PIB settings

```
.\hpavkey -L1 -D "1 HUB Unique Device Access Key!"
DBF40B772102DEDA70E14D58D4F5C093
.\modpib -D DBF40B772102DEDA70E14D58D4F5C093 -M 0000000000AA "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\Hub.pib"
```

### Unique Powerline Adapter 2 ModPib settings

```
.\hpavkey -L1 -D "1 PA2 Unique Device Access Key!"
47C4A054D905017F2FDDEFADAFCA1BA5
.\modpib -D 47C4A054D905017F2FDDEFADAFCA1BA5 -M 000000000002 "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\PA2.pib"
```


### Powerline Adapter 3 ModPib settings

```
.\hpavkey -L1 -D "1 PA3 Unique Device Access Key!"
C84F4ACA99B533AD8FB3B59D0D215CA2
.\modpib -D C84F4ACA99B533AD8FB3B59D0D215CA2 -M 000000000003 "C:\Users\admin1\Documents\Powerline Adapters\TPL-406E-firmware\fw_tpl-406ev2\PA3.pib"
```

