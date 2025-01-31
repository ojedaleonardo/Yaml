# 🚀 EC2 IMDSv2 Remediation Stack 🔒

Este stack de AWS CloudFormation configura un rol, una regla de AWS Config y una remediación automática para garantizar que todas las instancias EC2 en la cuenta utilicen **IMDSv2** (Instance Metadata Service Version 2).

## 📌 Descripción

Este stack realiza las siguientes acciones:

✅ **Crea un rol IAM** (`ec2-imdsv2-remediation`) que permite la ejecución de automatizaciones de AWS Systems Manager y acciones de AWS Config relacionadas con la configuración de instancias EC2.

✅ **Configura una regla de AWS Config** (`ec2-imdsv2-remediation`) para verificar si las instancias EC2 requieren IMDSv2.

✅ **Establece una configuración de remediación automática** en AWS Config, utilizando un documento de Systems Manager para modificar las opciones de metadatos de la instancia y requerir IMDSv2.

## 🔧 Requisitos previos

🔹 Permisos para desplegar stacks de AWS CloudFormation.
🔹 AWS Config habilitado en la cuenta.
🔹 AWS Systems Manager habilitado y configurado en las instancias EC2.

## 🚀 Implementación

Para desplegar este stack, sigue estos pasos:

1️⃣ **Desplegar el stack mediante la consola de AWS CloudFormation**:
   - Inicia sesión en la consola de AWS.
   - Navega a la sección de **AWS CloudFormation**.
   - Selecciona **"Crear stack"** > **"Con nueva plantilla"**.
   - Carga la plantilla `ec2-imdsv2-remediation.yml`.
   - Configura los parámetros y crea el stack.

2️⃣ **Desplegar el stack utilizando la CLI de AWS**:
   - Ejecuta el siguiente comando en la terminal:

     ```sh
     aws cloudformation create-stack --stack-name ec2-imdsv2-remediation \
       --template-body file://ec2-imdsv2-remediation.yml \
       --capabilities CAPABILITY_NAMED_IAM
     ```

3️⃣ **Verificar la implementación**:
   - Revisa el estado del stack en la consola de **CloudFormation**.
   - Confirma que la regla de **AWS Config** `ec2-imdsv2-remediation` aparece en la consola de AWS Config.
   - Asegúrate de que las instancias EC2 en la cuenta están cumpliendo con la política de **IMDSv2**.

## 🗑️ Eliminación del stack

Si necesitas eliminar el stack, usa el siguiente comando:

```sh
aws cloudformation delete-stack --stack-name ec2-imdsv2-remediation
```

## ℹ️ Notas adicionales

⚠️ **Este stack aplica la remediación de IMDSv2 de manera automática** en todas las instancias EC2 no conformes.
⚙️ Puedes modificar el número de intentos automáticos y el intervalo de reintento en la configuración de remediación (`MaximumAutomaticAttempts` y `RetryAttemptSeconds`).
💰 AWS Config puede generar costos adicionales dependiendo del uso y la cantidad de reglas configuradas en tu cuenta.

---

✨ ¡Con este stack, aseguras que todas las instancias EC2 en tu cuenta usen **IMDSv2** para mejorar la seguridad y prevenir ataques de metadatos! 🔐

📌 **Autor: Leonardo Ojeda**


