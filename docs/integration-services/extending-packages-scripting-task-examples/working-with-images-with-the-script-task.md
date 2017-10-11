---
title: "Utilizzo di immagini con l'attività Script | Documenti Microsoft"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- graphics [Integration Services]
- Script task [Integration Services], images
- Drawing namespace
- images [Integration Services]
- SSIS Script task, images
- Script task [Integration Services], examples
- thumbnails [Integration Services]
- System.Drawing namespace
- JPEG format [Integration Services]
- .jpeg files
ms.assetid: 74aeb7ab-51b2-4b9f-84ee-0b46a7908ab9
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4a28fe7c6024d8cf5669199e5f33e3532013e4d3
ms.contentlocale: it-it
ms.lasthandoff: 09/26/2017

---
# <a name="working-with-images-with-the-script-task"></a>Utilizzo di immagini con l'attività Script
  Un database di prodotti o utenti include di frequente immagini oltre a testo e dati numerici. Il **Drawing** dello spazio dei nomi in Microsoft .NET Framework fornisce classi per la modifica di immagini.  
  
 [Esempio 1: Convertire immagini in formato JPEG](#example1)  
  
 [Esempio 2: Creare e salvare le immagini di anteprima](#example2)  
  
> [!NOTE]  
>  Se si desidera creare un'attività da riutilizzare più facilmente con più pacchetti, è possibile utilizzare il codice di questo esempio di attività Script come punto iniziale per un'attività personalizzata. Per altre informazioni, vedere [Sviluppo di un'attività personalizzata](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
##  <a name="example1"></a>Descrizione dell'esempio 1: Convertire immagini in formato JPEG  
 Nell'esempio seguente viene aperto un file di immagine specificato da una variabile e lo salva come file JPEG compresso tramite un codificatore. Il codice per recuperare le informazioni sul codificatore viene incapsulato in una funzione privata.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-a-single-image-file"></a>Per configurare questa attività Script di esempio per l'utilizzo con un solo file di immagine  
  
1.  Creare una variabile di stringa denominata `CurrentImageFile` e impostarne il valore sul percorso e sul nome di un file di immagine esistente.  
  
2.  Nel **Script** pagina del **Editor attività Script**, aggiungere il `CurrentImageFile` variabile il **ReadOnlyVariables** proprietà.  
  
3.  Nel progetto di script, impostare un riferimento al **Drawing** dello spazio dei nomi.  
  
4.  Nel codice, utilizzare **importazioni** istruzioni per importare il **Drawing** e **System.IO** gli spazi dei nomi.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-multiple-image-files"></a>Per configurare questa attività Script di esempio per l'utilizzo con più file di immagine  
  
1.  Inserire l'attività Script all'interno di un contenitore Ciclo Foreach.  
  
2.  Nel **raccolta** pagina del **Editor ciclo Foreach**, selezionare il **Foreach File Enumerator** come enumeratore e specificare il percorso e il filtro dell'origine file, ad esempio come "*.bmp".  
  
3.  Nel **mapping variabili** pagina, eseguire il mapping di `CurrentImageFile` variabile all'indice 0. Questa variabile passa il nome file corrente all'attività Script a ogni iterazione dell'enumeratore.  
  
    > [!NOTE]  
    >  Questi passaggi vengono aggiunti a quelli elencati nella procedura per l'utilizzo con un solo file di immagine.  
  
### <a name="example-1-code"></a>Codice di esempio 1  
  
```vb  
Public Sub Main()  
  
    'Create and initialize variables.  
    Dim currentFile As String  
    Dim newFile As String  
    Dim bmp As Bitmap  
    Dim eps As New Imaging.EncoderParameters(1)  
    Dim ici As Imaging.ImageCodecInfo  
    Dim supportedExtensions() As String = _  
        {".BMP", ".GIF", ".JPG", ".JPEG", ".EXIF", ".PNG", _  
        ".TIFF", ".TIF", ".ICO", ".ICON"}  
  
    Try  
        'Store the variable in a string for local manipulation.  
        currentFile = Dts.Variables("CurrentImageFile").Value.ToString  
        'Check the extension of the file against a list of  
        'files that the Bitmap class supports.  
        If Array.IndexOf(supportedExtensions, _  
            Path.GetExtension(currentFile).ToUpper) > -1 Then  
  
            'Load the file.  
            bmp = New Bitmap(currentFile)  
  
            'Calculate the new name for the compressed image.  
            'Note: This will overwrite existing JPEGs.  
            newFile = Path.Combine( _  
                Path.GetDirectoryName(currentFile), _  
                String.Concat(Path.GetFileNameWithoutExtension(currentFile), _  
                ".jpg"))  
  
            'Specify the compression ratio (0=worst quality, 100=best quality).  
            eps.Param(0) = New Imaging.EncoderParameter( _  
                Imaging.Encoder.Quality, 75)  
  
            'Retrieve the ImageCodecInfo associated with the jpeg format.  
            ici = GetEncoderInfo("image/jpeg")  
  
            'Save the file, compressing it into the jpeg encoding.  
            bmp.Save(newFile, ici, eps)  
        Else  
            'The file is not supported by the Bitmap class.  
            Dts.Events.FireWarning(0, "Image Resampling Sample", _  
                "File " & currentFile & " is not a supported format.", _  
                "", 0)  
         End If  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        'An error occurred.  
        Dts.Events.FireError(0, "Image Resampling Sample", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
  
Private Function GetEncoderInfo(ByVal mimeType As String) As Imaging.ImageCodecInfo  
  
    'The available image codecs are returned as an array,  
    'which requires code to iterate until the specified codec is found.  
  
    Dim count As Integer  
    Dim encoders() As Imaging.ImageCodecInfo  
  
    encoders = Imaging.ImageCodecInfo.GetImageEncoders()  
  
    For count = 0 To encoders.Length  
        If encoders(count).MimeType = mimeType Then  
            Return encoders(count)  
        End If  
    Next  
  
    'This point is only reached if a codec is not found.  
    Err.Raise(513, "Image Resampling Sample", String.Format( _  
        "The {0} codec is not available. Unable to compress file.", _  
            mimeType))  
    Return Nothing  
  
End Function  
  
```  
  
##  <a name="example2"></a>Descrizione dell'esempio 2: Creare e salvare le immagini di anteprima  
 Nell'esempio seguente viene aperto un file di immagine specificato da una variabile, viene creata un'anteprima dell'immagine pur mantenendo una proporzione costante e viene salvata l'anteprima con un nome file modificato. Il codice che calcola l'altezza e larghezza dell'anteprima mantenendo una proporzione costante viene incapsulato in una subroutine privata.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-a-single-image-file"></a>Per configurare questa attività Script di esempio per l'utilizzo con un solo file di immagine  
  
1.  Creare una variabile di stringa denominata `CurrentImageFile` e impostarne il valore sul percorso e sul nome di un file di immagine esistente.  
  
2.  Creare anche la variabile di tipo integer `MaxThumbSize` e assegnare un valore in pixel, ad esempio 100.  
  
3.  Nel **Script** pagina del **Editor attività Script**, aggiungere entrambe le variabili per il **ReadOnlyVariables** proprietà.  
  
4.  Nel progetto di script, impostare un riferimento al **Drawing** dello spazio dei nomi.  
  
5.  Nel codice, utilizzare **importazioni** istruzioni per importare il **Drawing** e **System.IO** gli spazi dei nomi.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-multiple-image-files"></a>Per configurare questa attività Script di esempio per l'utilizzo con più file di immagine  
  
1.  Inserire l'attività Script all'interno di un contenitore Ciclo Foreach.  
  
2.  Nel **raccolta** pagina del **Editor ciclo Foreach**, selezionare il **Foreach File Enumerator** come il **enumeratore**e specificare il percorso e il filtro dei file di origine, ad esempio "*.jpg".  
  
3.  Nel **mapping variabili** pagina, eseguire il mapping di `CurrentImageFile` variabile all'indice 0. Questa variabile passa il nome file corrente all'attività Script a ogni iterazione dell'enumeratore.  
  
    > [!NOTE]  
    >  Questi passaggi vengono aggiunti a quelli elencati nella procedura per l'utilizzo con un solo file di immagine.  
  
### <a name="example-2-code"></a>Codice di esempio 2  
  
```vb  
Public Sub Main()  
  
    Dim currentImageFile As String  
    Dim currentImage As Image  
    Dim maxThumbSize As Integer  
    Dim thumbnailImage As Image  
    Dim thumbnailFile As String  
    Dim thumbnailHeight As Integer  
    Dim thumbnailWidth As Integer  
  
    currentImageFile = Dts.Variables("CurrentImageFile").Value.ToString  
    thumbnailFile = Path.Combine( _  
        Path.GetDirectoryName(currentImageFile), _  
        String.Concat(Path.GetFileNameWithoutExtension(currentImageFile), _  
        "_thumbnail.jpg"))  
  
    Try  
        currentImage = Image.FromFile(currentImageFile)  
  
        maxThumbSize = CType(Dts.Variables("MaxThumbSize").Value, Integer)  
        CalculateThumbnailSize( _  
            maxThumbSize, currentImage, thumbnailWidth, thumbnailHeight)  
  
        thumbnailImage = currentImage.GetThumbnailImage( _  
           thumbnailWidth, thumbnailHeight, Nothing, Nothing)  
        thumbnailImage.Save(thumbnailFile)  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        Dts.Events.FireError(0, "Script Task Example", _  
        ex.Message & ControlChars.CrLf & ex.StackTrace, _  
        String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
  
Private Sub CalculateThumbnailSize( _  
    ByVal maxSize As Integer, ByVal sourceImage As Image, _  
    ByRef thumbWidth As Integer, ByRef thumbHeight As Integer)  
  
    If sourceImage.Width > sourceImage.Height Then  
        thumbWidth = maxSize  
        thumbHeight = CInt((maxSize / sourceImage.Width) * sourceImage.Height)  
    Else  
        thumbHeight = maxSize  
        thumbWidth = CInt((maxSize / sourceImage.Height) * sourceImage.Width)  
    End If  
  
End Sub  
```  
  
```csharp  
bool ThumbnailCallback()  
        {  
            return false;  
        }  
        public void Main()  
        {  
  
            string currentImageFile;  
            Image currentImage;  
            int maxThumbSize;  
            Image thumbnailImage;  
            string thumbnailFile;  
            int thumbnailHeight = 0;  
            int thumbnailWidth = 0;  
  
            currentImageFile = Dts.Variables["CurrentImageFile"].Value.ToString();  
            thumbnailFile = Path.Combine(Path.GetDirectoryName(currentImageFile), String.Concat(Path.GetFileNameWithoutExtension(currentImageFile), "_thumbnail.jpg"));  
  
            try  
            {  
  
                currentImage = Image.FromFile(currentImageFile);  
  
                maxThumbSize = (int)Dts.Variables["MaxThumbSize"].Value;  
                CalculateThumbnailSize(maxThumbSize, currentImage, ref thumbnailWidth, ref thumbnailHeight);  
  
                Image.GetThumbnailImageAbort myCallback = new Image.GetThumbnailImageAbort(ThumbnailCallback);  
  
                thumbnailImage = currentImage.GetThumbnailImage(thumbnailWidth, thumbnailHeight, ThumbnailCallback, IntPtr.Zero);  
                thumbnailImage.Save(thumbnailFile);  
                Dts.TaskResult = (int)ScriptResults.Success;  
            }  
            catch (Exception ex)  
            {  
                Dts.Events.FireError(0, "Script Task Example", ex.Message + "\r" + ex.StackTrace, String.Empty, 0);  
                Dts.TaskResult = (int)ScriptResults.Failure;  
            }  
  
        }  
  
        private void CalculateThumbnailSize(int maxSize, Image sourceImage, ref int thumbWidth, ref int thumbHeight)  
        {  
  
            if (sourceImage.Width > sourceImage.Height)  
            {  
                thumbWidth = maxSize;  
                thumbHeight = (int)(sourceImage.Height * maxSize / sourceImage.Width);  
            }  
            else  
            {  
                thumbHeight = maxSize;  
                thumbWidth = (int)(sourceImage.Width * maxSize / sourceImage.Height);  
  
            }  
  
        }  
  
```  
  
  