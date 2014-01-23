It's helpful to ignore incidental changes to configuration such as `Makefile.config` so that only substantive and deliberate changes are versioned.

To ignore your personal changes run

     git update-index --assume-unchanged Makefile.config

and to repeal the ignore run

     git update-index --no-assume-unchanged Makefile.config

and so on for any other configuration files.