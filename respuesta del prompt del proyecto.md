¡Excelente iniciativa! Vamos a construir el ecosistema **.agents** para **Spideysaurus**. Este enfoque estructurado no solo organiza tu código, sino que dota a tu proyecto de una mentalidad de "agente" donde cada habilidad (diseño, código, scraping) tiene su propio espacio.

---

## 1. Estructura de la Habilidad Agente Global: `.agents`

Primero, configuramos la raíz de tus agentes para que el sistema reconozca las habilidades disponibles.

**Carpeta raíz:** `.agents/`

### Archivo: `SKILL.md`
```markdown
# Global Agent Skill: Spideysaurus Ecosystem
Este agente coordina las automatizaciones para la tienda de dinosaurios.

## Habilidades (Skills)
- **Design Skill**: Manejo de UI/UX y Branding.
- **Code Skill**: Lógica de negocio en Dart y CRUD.
- **Scraping Skill**: Recolección de datos de precios de mercado.

## Estructura
- /scripts: Automatizaciones de despliegue.
- /ejemplos: Blueprints de widgets.
- /resources: Assets y modelos de datos JSON.
```

---

## 2. Prerrequisitos y Configuración del Entorno

Antes de tocar código, aseguremos que el motor esté encendido.

### Verificación de Herramientas
Ejecuta esto en tu terminal (VS Code / Antigravity):
1. **Flutter:** `flutter --version` (Si no está, descárgalo en [flutter.dev](https://docs.flutter.dev/get-started/install)).
2. **Firebase CLI:** `firebase --version`. Si no lo tienes:
   * `npm install -g firebase-tools`
3. **Login:** `firebase login` (Sigue el flujo en el navegador).

### Conexión con Firebase Console
1. Crea un proyecto en [Firebase Console](https://console.firebase.google.com/) llamado `Spideysaurus`.
2. Habilita **Cloud Firestore** en modo de prueba.
3. Registra tu app (Android) y descarga el archivo `google-services.json` en `android/app/`.

---

## 3. Creación del Proyecto: `proyectoSpideysaurus`

Genera la base del proyecto desde la terminal:
```bash
flutter create proyectoSpideysaurus
cd proyectoSpideysaurus
```

### Configuración de `pubspec.yaml`
Añade las dependencias necesarias para Firebase y la gestión de estado:
```yaml
dependencies:
  flutter:
    sdk: flutter
  firebase_core: ^3.0.0
  cloud_firestore: ^5.0.0
  cupertino_icons: ^1.0.6
```
*Ejecuta `flutter pub get` después de guardar.*

---

## 4. Implementación del CRUD Spideysaurus

Organizaremos el código siguiendo la lógica de los agentes.

### A. Modelo de Datos (`lib/models/toy_model.dart`)
```dart
class Toy {
  String id;
  String nombre;
  String especie;
  double precio;

  Toy({required this.id, required this.nombre, required this.especie, required this.precio});

  Map<String, dynamic> toMap() => {
    "nombre": nombre,
    "especie": especie,
    "precio": precio,
  };

  factory Toy.fromFirestore(Map<String, dynamic> data, String id) {
    return Toy(
      id: id,
      nombre: data['nombre'] ?? '',
      especie: data['especie'] ?? '',
      precio: (data['precio'] ?? 0).toDouble(),
    );
  }
}
```

### B. Servicio Firestore (`lib/services/firebase_service.dart`)
```dart
import 'package:cloud_firestore/cloud_firestore.dart';
import '../models/toy_model.dart';

class FirebaseService {
  final CollectionReference toysRef = FirebaseFirestore.instance.collection('juguetes');

  // Create
  Future<void> addToy(Toy toy) => toysRef.add(toy.toMap());

  // Read
  Stream<List<Toy>> getToys() {
    return toysRef.snapshots().map((snapshot) =>
        snapshot.docs.map((doc) => Toy.fromFirestore(doc.data() as Map<String, dynamic>, doc.id)).toList());
  }

  // Update
  Future<void> updateToy(Toy toy) => toysRef.doc(toy.id).update(toy.toMap());

  // Delete
  Future<void> deleteToy(String id) => toysRef.doc(id).delete();
}
```

### C. UI: Pantalla de Listado y Formulario (`lib/screens/home_screen.dart`)
```dart
import 'package:flutter/material.dart';
import '../services/firebase_service.dart';
import '../models/toy_model.dart';

class HomeScreen extends StatelessWidget {
  final FirebaseService _service = FirebaseService();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      app_appBar: AppBar(title: Text("Spideysaurus Shop 🦖")),
      body: StreamBuilder<List<Toy>>(
        stream: _service.getToys(),
        builder: (context, snapshot) {
          if (!snapshot.hasData) return Center(child: CircularProgressIndicator());
          final toys = snapshot.data!;
          return ListView.builder(
            itemCount: toys.length,
            itemBuilder: (context, index) {
              return ListTile(
                title: Text(toys[index].nombre),
                subtitle: Text(toys[index].especie),
                trailing: IconButton(
                  icon: Icon(Icons.delete, color: Colors.red),
                  onPressed: () => _service.deleteToy(toys[index].id),
                ),
              );
            },
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () => _showAddDialog(context),
        child: Icon(Icons.add),
      ),
    );
  }

  void _showAddDialog(BuildContext context) {
    // Aquí iría el controlador de texto y la lógica para crear un nuevo dinosaurio
  }
}
```

---

## 5. Verificación de Funcionalidad

Para asegurar que todo funcione bajo el estándar de tu agente global:

1.  **Check de Conectividad:** Inicia el emulador y corre `flutter run`.
2.  **Prueba Firestore:** Agrega un dato manualmente desde la consola de Firebase y verifica que aparezca en la app en tiempo real (gracias al `StreamBuilder`).
3.  **Log de Agente:** Revisa la carpeta `.agents/scripts` y crea un archivo `check_env.sh` que verifique las versiones de las herramientas automáticamente.

### Estructura Final de Archivos:
```text
proyectoSpideysaurus/
├── .agents/
│   ├── SKILL.md
│   ├── scripts/
│   ├── ejemplos/
│   └── resources/
├── lib/
│   ├── models/
│   ├── screens/
│   ├── services/
│   └── main.dart
├── pubspec.yaml
└── android/app/google-services.json
```

¿Deseas que profundice en el código de la **Skill de Scraping** para capturar precios de dinosaurios de otras tiendas o prefieres terminar de pulir la UI del CRUD?
