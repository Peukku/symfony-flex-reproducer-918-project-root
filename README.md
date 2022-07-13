# Test project for issue 918 in symfony/flex

Issue: https://github.com/symfony/flex/issues/918

Steps to reproduce Case A, project in subfolder:

```
git clone https://github.com/Peukku/symfony-flex-reproducer-918-project-root.git
cd symfony-flex-reproducer-918-project-root/project-A
symfony composer install
symfony composer recipes:update symfony/framework-bundle
```

Result:
```
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
 	deleted:    projectB/config/bootstrap.php
	deleted:    projectB/config/packages/test/framework.yaml
	deleted:    projectB/config/routes/dev/framework.yaml
	modified:   projectB/symfony.lock
```

Expected Result:
```
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   projectB/.env
	deleted:    projectB/config/bootstrap.php
	modified:   projectB/config/packages/framework.yaml
	deleted:    projectB/config/packages/test/framework.yaml
	modified:   projectB/config/preload.php
	deleted:    projectB/config/routes/dev/framework.yaml
	new file:   projectB/config/routes/framework.yaml
	modified:   projectB/config/services.yaml
	modified:   projectB/public/index.php
	modified:   projectB/src/Kernel.php
	modified:   projectB/symfony.lock
```

Steps to reproduce Case B, project in git subproject:
```
git clone https://github.com/Peukku/symfony-flex-reproducer-918-project-root.git
cd symfony-flex-reproducer-918-project-root/project-B
git submodule init
git submodule update
symfony composer install
symfony composer recipes:update symfony/framework-bundle
```
Result:
```
  Updating recipe for symfony/framework-bundle...

There was an error applying the recipe update patch
Failed to create "./.git/objects/49": mkdir(): Not a directory
```
