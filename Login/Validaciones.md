# Validaciones formulario

```dart

import 'package:flutter/services.dart';

class Validators {

  static String? email( String? value ) {

    String pattern = r'^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$';
    
    RegExp regExp  = RegExp(pattern);

    return regExp.hasMatch(value ?? '' )
      ? null
      : 'Email no válido';
  }

  static String? pass( String? value ) {
    return ( value != null && value.length >= 6 )
      ? null
      : 'Debe tener minimo 6 caracteres';
  }

  static FilteringTextInputFormatter inputFormatDouble(){
    return FilteringTextInputFormatter.allow(RegExp(r'^(\d+)?\.?\d{0,2}'));
  }

}
```
