# Upload de fichier

## ajouter-paquet.xhtml :

``` html
<h:form enctype="multipart/form-data"> 
	<p:fileUpload value="#{cataloguePageBean.file}" mode="simple" skinSimple="true" 
	/> 

 <p:commandButton  actionListener="#{cataloguePageBean.ajouterPaquet()}" 
                                ajax="false"
                                action="lister-paquets.xhtml?faces-redirect=true" />
</h:form>
```

## AjouterPaquetBean.java :
```
@Getter
@Setter
private UploadedFile file;

public void ajouterPaquet() {
	byte[] data = file.getContents(); // important
	nouveauPaquet.setImage(data); // important
	daoPaquet.create(nouveauPaquet);
	nouveauPaquet = CDI.current().select(Paquet.class).get();
}
```


