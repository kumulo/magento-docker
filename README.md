# magento-docker

## Prepare

Pull Magento in project directory

    git pull https://github.com/magento/magento2.git ./project

Up docker

    docker-compose up -d

## Install Magento
Dependancies

    composer install
Magento base setup

    bin/magento setup:install --base-url=http://localhost:82/ \
	     --db-host=mysql --db-name=magento \
	     --db-user=root --db-password=passwd \
	     --admin-firstname=Magento --admin-lastname=User --admin-email=user@example.com \
	     --admin-user=admin --admin-password=admin123 --language=fr_FR \
	     --currency=EUR --timezone=Europe/Paris --cleanup-database \
	     --sales-order-increment-prefix="ORD$" --session-save=db --use-rewrites=1
Magento compile

    bin/magento setup:di:compile
