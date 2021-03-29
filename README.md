# WordPress PHP-FPM Nginx Helm Chart
A Helm Chart for running WordPress with PHP-FPM behind Nginx under Kubernetes.

Features:

* A persistent volume is created and mounted to '/var/www/html/wp-content/'.
* The chart supports creating multiple ingresses.
* WP-CLI is available under '/usr/local/bin/wp'. After entering the command, wp-cli is downloaded and run on the fly.
* The chart doesn't bring a MariaDB/MySQL deployment with it. You have to create a database and point WordPress to it.
* After WordPress startup file permissions of 'wp-config.php' are changed to read-only to prevent editing by plugins.

The folder 'deployments' contains a test deployment that can be installed with:

    # helm install wp-test ./wordpress/ -n default -f deployments/test.yaml

The the deployment consists of three containers:

* WordPress FPM version,
* Nginx,
* WordPress FPM version as Init-Container.
 
When the Pod is started an Init-Container automatically copies the WordPress source into an emptyDir volume to make it available to the Nginx container.
