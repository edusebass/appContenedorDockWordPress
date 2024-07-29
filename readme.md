- maestro

CREATE USER 'replica'@'%' IDENTIFIED BY 'replica_password';
GRANT REPLICATION SLAVE ON . TO 'replica'@'%';
SHOW MASTER STATUS

- esclavo

-- Configura el esclavo para conectarse al maestro
CHANGE MASTER TO
MASTER_HOST = 'wordpress-db',
MASTER_USER = 'replica',
MASTER_PASSWORD = 'replica_password',
MASTER_LOG_FILE = 'mysql-bin.000001', -- Usa el archivo de log binario obtenido del maestro
MASTER_LOG_POS = 4; -- Usa la posición obtenida del maestro

-- Inicia el proceso de replicación
START SLAVE;

-- Verifica el estado de la replicación
SHOW SLAVE STATUS;
