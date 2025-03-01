

Presentamos el laboratorio en el cual desarrollamos un despliegue automátizado de WordPress con terraform, con acceso automático a nuestro wordPress.

La arquitectura implementada consta de los siguientes componentes principales:

Red (VPC):

VPC con dos zonas de disponibilidad
Subredes públicas y privadas en cada zona
Internet Gateway para acceso a internet
NAT Gateway para que las instancias privadas accedan a internet

Balanceadores de Carga (ALB):

ALB Externo en subredes públicas que maneja el tráfico entrante HTTPS (443) y redirecciona HTTP (80) a HTTPS
ALB Interno en subredes privadas que distribuye el tráfico a las instancias WordPress

Compute (EC2):

Auto Scaling Group con instancias WordPress en subredes privadas
Launch Template con configuración de WordPress y dependencias
Montaje de EFS para almacenamiento compartido
Configuración automática de WordPress mediante user data

Almacenamiento:

RDS PostgreSQL para la base de datos de WordPress
EFS para almacenamiento compartido de archivos WordPress
ElastiCache Redis para caché de objetos
Uso de snapshot RDS para restaurar configuración preexistente de WordPress

Seguridad:

Grupos de seguridad específicos para cada componente
ACM para certificado SSL/TLS
IAM roles y políticas para permisos EC2

Monitoreo:

CloudWatch Logs para registros
Alarmas CloudWatch para:
CPU alta en EC2
CPU y almacenamiento en RDS
CPU y memoria en ElastiCache
La arquitectura está diseñada para ser altamente disponible, escalable y segura, utilizando servicios gestionados de AWS.

Limitaciones:

a) Backup y Restauración:

Se implementó la restauración desde un snapshot de RDS existente
Esto permite preservar toda la configuración previa de WordPress
El snapshot contiene la estructura de la base de datos y los datos
Facilita la migración y el despliegue manteniendo la configuración existente


b) AMI

La AMI que se usa en el proyecto fue una AMI personalizada 
Instalamos todo lo necesario para que el WordPress se desplegase 
A la hora de generar nuevas instancias el proceso es más rápido

