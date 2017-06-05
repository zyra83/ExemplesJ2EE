# FlashScope


## Lister paquets.xhtml :

- formulaire autour du datatable
- fonctionne avec un command Link
```
<h:commandLink actionListener="#{listerPaquetsFlashScopePageBean.mettrePaquetFlashScope(p)}"
					                    action="voir-paquet-flash-scope.xhtml?faces-redirect=true" 
					                    value="#{p.libelle}" />
```

## ListePaquetBean.java

```
// La constante
public static final String FLASH_PARAM_PAQUET = "paquet_selectionne";

// la mise en FlashScope du paquet
public void mettrePaquetFlashScope(Paquet p) {
	JsfUtils.putInFlashScope(FLASH_PARAM_PAQUET, p);
}
```

## voir-paquet-flash-scope.xhtml
Page qui reçoit l'objet du FlashScope.

```
<h:outputText value="#{voirPaquetFlashScopePageBean.paquet.id}" />
```

## VoirPaquetFlashScopePageBean.java
Récupère le paquet depuis le flash scope et fournit l'objet à afficher à la page.
``` java
@Getter
@Setter
Paquet paquet;

@PostConstruct
public void init() {

	paquet = (Paquet) JsfUtils.getFromFlashScope(ListerPaquetsFlashScopePageBean.FLASH_PARAM_PAQUET);

}
```