no all file in dir ./terraform in ALLDIR 

ALLDIR / .terraform

no all tfstate file LOCALDIR and LOCALDIR-1

LOCALDIR / *.tfstate
LOCALDIR / *.tfstate
LOCALDIR /LOCALDIR-1 / *.tfstate
LOCALDIR /LOCALDIR-1 / *.tfstate.*  ( e.g.  1.tfstate.gz,all.tfstate.bak)

no all crash.log file in LOCALDIR

LOCALDIR / crash.log
LOCALDIR / crash.*.log  (e.g. crash.1.log, crash.all.log)

no all tfvars and tfvars.json file in LOCALDIR  and LOCALDIR-1

LOCALDIR / *.tfvars
LOCALDIR / *.tfvars.json
LOCALDIR /LOCALDIR-1 / *.tfvars
LOCALDIR /LOCALDIR-1 / *.tfvars.json  ( e.g.  1.tfvars.json,all.tfvars)
 
no all override.tf and  override.tf.json in LOCALDIR

LOCALDIR / override.tf
LOCALDIR / override.tf.json

no all *_override.tf and *_override.tf.json in LOCALDIR  and LOCALDIR-1

LOCALDIR / *_override.tf
LOCALDIR / *_override.tf.json
LOCALDIR /LOCALDIR-1 / *_override.tf
LOCALDIR /LOCALDIR-1 / *_override.tf.json  ( e.g.  1_override.tf.json,all_override.tf)

no terraform.rc and .terraformrc file in LOCALDIR

LOCALDIR / .terraformrc
LOCALDIR / terraform.rc
