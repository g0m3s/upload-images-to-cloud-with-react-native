Estou a escrever este pequeno artigo pois recentemente encontrei certa dificuldade para conseguir realizar esta tarefa. ...............completar.............

- Adicionar o [react-native-image-crop-picker](https://github.com/ivpusic/react-native-image-crop-picker) (ele permite que o usuário consiga adicinar fotos que estão em sua galeria)
- Adicionar o [react-native-image-resizer](https://github.com/bamlab/react-native-image-resizer) (como o nome sugere, permite fazer uma modificação no tamanha da imagem que será posteriormente enviada para a nuvem, além de permitir uma compressão, diminuindo o tamanho da imagem final)
- Adicionar o [react-native-image-base64](https://www.npmjs.com/package/react-native-image-base64) (vai permitir a codificação)

Bom, vou começar com o código inteiro e depois o explicarei por partes, fechô?

import React from 'react'
import { View, TouchableOpacity, Text } from 'react-native'

import ImagePicker from 'react-native-image-crop-picker'
import ImageResizer from 'react-native-image-resizer'
import ImgToBase64 from 'react-native-image-base64'

export default function App () {

function uploadImageToCloud (images) {

ImageResizer.createResizedImage(images[0].path, 80, 80, 'JPEG', 50)
.then(res => {

```
    ImgToBase64.getBase64String(res.path)
    .then(base64String => uploadWorkImages(base64String))
    .catch(err => console.log(err));

    })
    .catch(err => {

        console.log(err)

    });

}

function uploadWorkImages (path) {

    let newImage = `data:jpeg;base64,${path}`

    const data = new FormData()
    data.append('file',newImage)
    data.append('upload_preset','testup')
    data.append("cloud_name","pdsgij")

    fetch("https://api.cloudinary.com/v1_1/pdsgij/upload", {

        method: 'POST',
        body: data

    })
    // .then( async res => { dataResult = await res.json() } )
    .then( async res=> await res.json() )
    .then(data=>{
        console.log(data)
    })
```

}

}