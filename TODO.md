# TODO

* add unprivileged user during installation and run every instance as that uid
* logrotate the logfiles

# Notes for upstream devs:

* Don't strip leading slash from -config= ; I think this is a recent regression.
  (/etc symlink hack)
* No `passwordAdmin` in .cfg should mean not possible to login! (default pwd in cfg)
* Don't write player/, arma2oa.cfg, core, and other garbage to assets directory
  (not a big deal unless multiple instances colliding matters)
* `logFile` in .cfg should not need to be changed for every cfg.
* server icon yellow for linux DSes again (was fixed i thought)
* How about the client doesn't crash when a selected server is restarted or goes offline??
* single ban.txt
