- maestro

GRANT ALL PRIVILEGES ON _._ TO 'replica'@'%' IDENTIFIED BY 'replica_password';

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

234ert78\*

/_ Servers configuration _/
$i = 0;

/_ First server _/
$i++;
$cfg['Servers'][$i]['host'] = 'wordpress-db'; // Maestro
$cfg['Servers'][$i]['user'] = 'root';
$cfg['Servers'][$i]['password'] = 'root';
$cfg['Servers'][$i]['auth_type'] = 'config';

/_ Second server _/
$i++;
$cfg['Servers'][$i]['host'] = 'mysql-slave'; // Esclavo
$cfg['Servers'][$i]['user'] = 'root';
$cfg['Servers'][$i]['password'] = 'root';
$cfg['Servers'][$i]['auth_type'] = 'config';

/_ End of servers configuration _/
$cfg['ServerDefault'] = 1; // Define el servidor predeterminado
