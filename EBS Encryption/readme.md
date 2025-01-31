EBS Encryption

Este repositorio contiene dos stacks de AWS CloudFormation para habilitar la encriptación de volúmenes EBS de manera automática mediante AWS Config y AWS Systems Manager (SSM).

Descripción de los Stacks

UnencryptedVolumes.yaml

Crea la IAM Role EncryptionRemediationRole con los permisos necesarios para manejar la encriptación de volúmenes.

Crea una Managed Policy EncryptEBSAutomationRole-policy con permisos para:

Operaciones de CloudFormation (crear, describir y eliminar stacks).

Operaciones de EC2 (crear y adjuntar volúmenes, gestionar snapshots, modificar atributos de instancias, etc.).

Operaciones de Lambda (crear, eliminar e invocar funciones).

Uso de claves KMS para cifrado y descifrado de datos.

IAM para gestionar roles y permisos relacionados con la automatización de EBS.

Exporta los valores del ARN de la role y el ID de la clave KMS.

ConfigSSM.yaml

Crea una regla de AWS Config (encrypted-volumes) que monitorea si los volúmenes EBS están encriptados.

Crea un documento de automatización de SSM (ENCRYPTunencryptedebsvolume) que remedia volúmenes no encriptados.

Configura AWS Config para iniciar la automatización de remediación.

Importa los valores de la IAM Role y la KMS Key generados en UnencryptedVolumes.yaml.

Orden de Implementación

Para desplegar los stacks en el orden correcto, ejecuta:

Desplegar UnencryptedVolumes.yaml

aws cloudformation create-stack --stack-name UnencryptedVolumesStack \
--template-body file://UnencryptedVolumes.yaml \
--capabilities CAPABILITY_NAMED_IAM

Esperar a que finalice la creación del stack y obtener su nombre

aws cloudformation describe-stacks --stack-name UnencryptedVolumesStack

Desplegar ConfigSSM.yaml utilizando el nombre del stack anterior

aws cloudformation create-stack --stack-name ConfigSSMStack \
--template-body file://ConfigSSM.yaml \
--parameters ParameterKey=RoleKeyStackNameParameter,ParameterValue=UnencryptedVolumesStack \
--capabilities CAPABILITY_NAMED_IAM

Notas

Ambos stacks deben ejecutarse en la misma región de AWS.

ConfigSSM.yaml depende de los valores exportados por UnencryptedVolumes.yaml, por lo que es obligatorio ejecutarlo en segundo lugar.

Se recomienda verificar la configuración de AWS Config y SSM después de la implementación para asegurar que la automatización esté funcionando correctamente.

Licencia

Este proyecto se encuentra bajo la licencia MIT. Puedes modificar y distribuir el código según sea necesario.

Autores: Leonardo Ojeda
