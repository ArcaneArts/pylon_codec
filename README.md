Simply allows models to implement PylonCodec for usage with Pylon. This package is split because a lot of projects use their models in servers / dart packages which do not have flutter.

# Usage

```dart
import 'package:pylon_codec/pylon_codec.dart';

// A note class representing our data model
class Note implements PylonCodec<Note> {
  final int id;
  final String name;
  final String description;

  const Note({
    required this.id,
    required this.name,
    required this.description,
  });
  
  const Note.codec() : id = -1, name = "", description = "";
  
  ...

  // Encode
  @override
  String pylonEncode(Note value) => value.id.toString();

  // Decode
  @override
  Future<Note> pylonDecode(String value) async => notes[int.parse(value)];
}
```

Then register it

```dart
import 'package:pylon_codec/pylon_codec.dart';

void main() {
  registerPylonCodec(const Note.codec());
  
  // Now its usable
}
```