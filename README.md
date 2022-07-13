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
 	deleted:    config/bootstrap.php
	deleted:    config/packages/test/framework.yaml
	deleted:    config/routes/dev/framework.yaml
	modified:   symfony.lock
```

Expected Result:
```
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   .env
	deleted:    config/bootstrap.php
	modified:   config/packages/framework.yaml
	deleted:    config/packages/test/framework.yaml
	modified:   config/preload.php
	deleted:    config/routes/dev/framework.yaml
	new file:   config/routes/framework.yaml
	modified:   config/services.yaml
	modified:   public/index.php
	modified:   src/Kernel.php
	modified:   symfony.lock
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
