# Conventional Commits & Commitlint Configuration

## ¿Qué es Conventional Commits?

[Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) es una convención para escribir mensajes de commits de manera estructurada y significativa. Su objetivo es mejorar la legibilidad del historial de commits y facilitar la automatización en el desarrollo de software, como la generación de versiones semánticas.

### Formato de un Commit Convencional

El formato estándar de un commit convencional es:

```plaintext
tipo(área opcional): descripción breve

[Opcional] Cuerpo del commit con más detalles
[Opcional] Referencias a issues o tickets
```

Ejemplo:

```plaintext
feat(auth): agregar autenticación con JWT

Se implementó la autenticación basada en tokens JWT para mejorar la seguridad.
Closes #45
```

### Tipos de commits comunes

- **feat**: Nueva funcionalidad
- **fix**: Corrección de errores
- **docs**: Cambios en documentación
- **style**: Cambios de formato, sin afectar el código (espacios, comas, etc.)
- **refactor**: Reestructuración del código sin cambios en funcionalidad
- **test**: Agregar o modificar pruebas
- **chore**: Tareas de mantenimiento del proyecto

---

## Configuración de Commitlint

[Commitlint](https://commitlint.js.org/guides/getting-started.html) es una herramienta que valida que los mensajes de commit sigan la convención de Conventional Commits.

### Instalación

Ejecuta el siguiente comando para instalar `commitlint` y su configuración recomendada:

```sh
npm install --save-dev @commitlint/{config-conventional,cli}
```

### Configuración

1. Crea un archivo de configuración `.commitlintrc.json` en la raíz del proyecto:

```sh
echo "export default { extends: ['@commitlint/config-conventional'] };" > commitlint.config.js
```

2. Opcionalmente, si usas `commit-msg` como hook de Git, instala `husky` para ejecutar `commitlint` automáticamente:

```sh
npm install --save-dev husky
npx husky init
```

3. Agrega un hook para validar los mensajes de commit:

```sh
# Add commit message linting to commit-msg hook
echo "npx --no -- commitlint --edit \$1" > .husky/commit-msg
# Windows users should use ` to escape dollar signs
echo "npx --no commitlint --edit `$1" > .husky/commit-msg
```

4. Asegúrate de que `husky` se ejecute en cada clonación del repositorio, agregando lo siguiente en `package.json`:

```json
"scripts": {
  "prepare": "husky"
}
```

---

## Uso

Ahora, cada vez que intentes hacer un commit, `commitlint` validará que el mensaje siga la convención.

Ejemplo de commit válido:

```sh
git commit -m "fix(login): corregir error de validación en el formulario"
```

Si el mensaje no sigue el formato adecuado, `commitlint` mostrará un error y evitará el commit.

---

## Configuración del Prompt de Commitlint

Para mejorar la experiencia al escribir mensajes de commit, podemos utilizar el prompt interactivo de Commitlint:

### Instalación del prompt

```sh
npm install --save-dev @commitlint/prompt-cli
```

### Uso del prompt

Adiciona este shortcut a tus scripts del package.json

```json
{
  "scripts": {
    "commit": "commit"
  }
}
```

Luego ejecuta el commando:

```sh
git add .
npm run commit
```

Sigue los pasos para hacer un commit semántico.

---

## Configuración con `@commitlint/cz-commitlint`

También podemos usar `commitizen` con `@commitlint/cz-commitlint` para mejorar la generación de commits convencionales.

### Instalación

```sh
npm install --save-dev @commitlint/cz-commitlint commitizen inquirer@9
```

### Configuración en `package.json`

Agrega la siguiente configuración en `package.json`:

```json
 "scripts": {
    "commit": "git-cz"
  },
  "config": {
    "commitizen": {
      "path": "@commitlint/cz-commitlint"
    }
  }
```

### Uso de `commitizen`

Ejecuta el siguiente comando para iniciar el prompt interactivo de Commitizen:

```sh
git add .
npm run commit
```

Sigue los pasos para hacer un commit semántico.

---

## Conclusión

Seguir la convención de Conventional Commits ayuda a mantener un historial de commits limpio y comprensible, además de facilitar la automatización en la gestión del código. Usar `commitlint` junto con `husky`, `commitizen` y su prompt interactivo garantiza que todos los commits en tu proyecto sigan esta convención. 

