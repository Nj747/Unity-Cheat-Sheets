# Serialización de Información
Un serializador es un código que convierte los datos a cadenas de texto. En Unity podemos hacer esto de 3 formas:
## 1. PlayerPrefs
Este concepto sirve para almacenar referencias de objetos que querramos que persistan a lo largo de nuestro juego. 

Algunos ejemplos serían: 
- Configuración del Videojuego (Brillo, volumen, lenguaje, etc.)
- Atributos de NPCs
- Atributos sobre personalización de un jugador
- Estadísticas en general

## 2. XML (eXtensible Markup Language) y JSON (Javascript Object Notation)
Estos serializadores se utilizan para almacenar datos como cadenas de texto y además transmitir información. La ventaja es que es muy fácil de manipular por el usuario.

## 3. Binary Data
Otra forma de serialización que permite guardar datos en archivos binarios. 

---
## ¿Cuándo debo serializar?
En el caso de Unity hay tipos que no puedo almacenar directamente como Vector3, Vector2, Quaternion, ya que estos no son datos primitivos y 
por ende necesito llevarlos a un tipo primitivo para luego serializarlos y almacenar los datos en un archivo.
Solución usar una estructura:
```cs
public struct serializableVector3
{
  public float x;
  public float y;
  public float z;
}
```
---
### PlayerPrefs + JSON
```cs
public class GestorDeEstado
{
  public static void Guardar(Monobehaviour componente)
  {
    PlayerPrefs.SetString("slot",JsonUtility.ToJson(componente));
  }
  
  public static void Cargar(Monobehaviour componente)
  {
    JsonUtility.FromJsonOverwrite(PlayerPrefs.Getstring("slot"),componente);
  }
}
```
