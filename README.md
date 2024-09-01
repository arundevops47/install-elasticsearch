# Setup-elasticsearch


## Install and Run Elasticsearch on Windows

To install Elasticsearch on Windows, follow these steps:

### 1. Download Elasticsearch

[Download Elasticsearch](https://www.elastic.co/downloads/elasticsearch)

Download the latest version of Elasticsearch for Windows.

### 2. Extract the Downloaded Archive

Once downloaded, extract the ZIP file to your desired location, e.g., `C:\elasticsearch`.

### 3. Configure Elasticsearch (Optional)

Navigate to the `config` directory inside your Elasticsearch folder (`C:\elasticsearch\config`).

You can edit the `elasticsearch.yml` file to customize your configuration, such as setting cluster names, network settings, etc.

### 4. Set Password

If you want to add security:

1. Open a Command Prompt as Administrator.
2. Navigate to the `bin` directory inside your Elasticsearch folder:

    ```sh
    cd C:\elasticsearch\bin
    ```

3. Run the following command to set up passwords:

    ```sh
    elasticsearch-setup-passwords interactive
    ```

    You will be prompted to enter passwords as the process progresses.

    - Please confirm that you would like to continue [y/N] - `y`
    - Enter password for [elastic]: `password` <!-- (You can choose any password) -->
    - Reenter password for [elastic]: `password` <!-- (You can choose any password) -->
    - Enter password for [apm_system]: `password` <!-- (You can choose any password) -->
    - Reenter password for [apm_system]: `password` <!-- (You can choose any password) -->
    - Enter password for [kibana_system]: `password` <!-- (You can choose any password) -->
    - Reenter password for [kibana_system]: `password` <!-- (You can choose any password) -->
    - Enter password for [logstash_system]: `password` <!-- (You can choose any password) -->
    - Reenter password for [logstash_system]: `password` <!-- (You can choose any password) -->
    - Enter password for [beats_system]: `password` <!-- (You can choose any password) -->
    - Reenter password for [beats_system]: `password` <!-- (You can choose any password) -->
    - Enter password for [remote_monitoring_user]: `password` <!-- (You can choose any password) -->

### Using the Passwords

Once you've set up the passwords, you'll use these credentials whenever you're prompted by Elasticsearch or any associated service (like Kibana) to log in.

For instance, if you're accessing Elasticsearch via a web browser, you'll use the `elastic` user and the password you set during this process.

### Storing Passwords Securely

Make sure to securely store the passwords you set. They will be required for accessing Elasticsearch and other Elastic Stack components.

### Disable Security (Optional)

If you are in a development environment and you want to disable security features (not recommended for production):

1. Edit the `elasticsearch.yml` configuration file located in the `config` directory.

2. Add or update the following settings:

    ```yaml
    xpack.security.enabled: false
    ```




### 5. Run Elasticsearch

1. Go to `C:\elasticsearch\bin`.

2. Double-click on `elasticsearch.bat`.

   This will start Elasticsearch in the foreground, and you'll see logs in the Command Prompt.

### 6. Test the Installation

1. Open your web browser and navigate to [http://localhost:9200/](http://localhost:9200/).

2. Enter the following credentials:

   - Username: `elastic`
   - Password: `password`

   You should see a JSON response similar to:

    ```json
    {
      "name" : "your-node-name",
      "cluster_name" : "elasticsearch",
      "cluster_uuid" : "some-uuid",
      "version" : {
        "number" : "7.x.x",
        "build_flavor" : "default",
        "build_type" : "zip",
        "build_hash" : "some-hash",
        "build_date" : "date",
        "build_snapshot" : false,
        "lucene_version" : "8.x.x",
        "minimum_wire_compatibility_version" : "7.x.x",
        "minimum_index_compatibility_version" : "6.x.x"
      },
      "tagline" : "You Know, for Search"
    }
    ```

### 7. Install Elasticsearch as a Windows Service (Optional)

If you want Elasticsearch to run as a service on Windows:

1. Open a new Command Prompt as Administrator.

2. Navigate to the `bin` directory inside your Elasticsearch folder:

    ```sh
    cd C:\elasticsearch\bin
    ```

3. Run the following command to install Elasticsearch as a service:

    ```sh
    elasticsearch-service.bat install
    ```

4. Start the service:

    ```sh
    elasticsearch-service.bat start
    ```

   You can now manage Elasticsearch from the Windows Services manager.

### 8. Verify the Service Installation

1. Open the Services app (`services.msc`).

2. Look for Elasticsearch in the list of services. It should be running.


# Installation and Run Elasticsearch on Ubuntu

## Elasticsearch Version 8

1. Download the Elasticsearch tarball and its checksum:

    ```bash
    wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.6.1-linux-x86_64.tar.gz
    wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.6.1-linux-x86_64.tar.gz.sha512
    ```

2. Verify the checksum:

    ```bash
    shasum -a 512 -c elasticsearch-8.6.1-linux-x86_64.tar.gz.sha512 
    ```

3. Extract the tarball:

    ```bash
    tar -xzf elasticsearch-8.6.1-linux-x86_64.tar.gz
    ```

4. Navigate to the Elasticsearch directory:

    ```bash
    cd elasticsearch-8.6.1/ 
    ```

5. Set up environment variables by adding them to your `~/.bashrc` file:

    ```bash
    echo 'export ES_HOME="$HOME/elasticsearch-8.6.1/"' >> ~/.bashrc
    echo 'export PATH="$ES_HOME/bin:$PATH"' >> ~/.bashrc
    ```

6. Reload the shell configuration:

    ```bash
    exec $SHELL
    ```

7. Start Elasticsearch:

    ```bash
    elasticsearch
    ```

8. Open another terminal window and check if Elasticsearch is running by executing:

    ```bash
    curl -X GET 'http://localhost:9200'
    ```

## Check Elasticsearch in Browser

- To check if Elasticsearch is running, visit:

    ```
    http://localhost:9200
    ```

- To interact with a specific index:

    ```
    http://localhost:9200/<index_name>/_doc/<id>
    ```

    Example:

    ```
    http://localhost:9200/books/_doc/1
    ```

## Delete an Index

- To delete an index, use:

    ```bash
    curl -X DELETE 'http://localhost:9200/<name_of_index>'
    ```

    Example:

    ```bash
    curl -X DELETE 'http://localhost:9200/books'
    ```


