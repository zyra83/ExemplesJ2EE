- Dans WebContent/resources/etrs/
- Créer le fichier monComposant.xhtml
- copier coller le merdier ci-dessous :

``` html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
	<html xmlns="http://www.w3.org/1999/xhtml"
		xmlns:composite="http://java.sun.com/jsf/composite"
		xmlns:ui="http://java.sun.com/jsf/facelets"
		xmlns:f="http://java.sun.com/jsf/core"
		xmlns:h="http://java.sun.com/jsf/html"
		xmlns:p="http://primefaces.org/ui">
<!-- 1er composant -->
<composite:interface>
	<composite:attribute name="actionListener" required="true"
		method-signature="void actionListener()" targets="boutonAjouter" />
	<composite:attribute name="title"></composite:attribute>
</composite:interface>

<composite:implementation>
<div class="form-group">
		<div class="col-sm-offset-2 col-sm-10">
	<p:commandButton id="boutonAjouter" class="btn btn-primary"
		value="Ajouter" icon="fa-plus"
		update="@form #{cc.attrs.additionalUpdate}" />
			</div>
	</div>
</composite:implementation>

<!-- 2eme composant -->
<composite:interface>
	<composite:attribute name="actionListener" required="true"
		method-signature="void actionListener()" targets="boutonAjouter" />
	<composite:attribute name="action" required="true"
		method-signature="java.lang.String action()" targets="boutonAjouter" />
	<composite:attribute name="additionalUpdate" />
	<composite:attribute name="ajax" default="true" />
</composite:interface>

<composite:implementation>
	<p:commandButton 
		id="boutonAjouter" 
		class="btn btn-primary"
		value="Ajouter" 
		ajax="#{cc.attrs.ajax}"
		update="@form #{cc.attrs.additionalUpdate}" />
</composite:implementation>

<!-- 3eme composant -->
<composite:interface>
	<composite:attribute name="title" required="true" />
	<composite:attribute name="enctype" default="application/x-www-form-urlencoded" />
</composite:interface>

<composite:implementation>
	<fieldset>
		<legend>
			<h:outputText value="#{cc.attrs.title}" />
		</legend>
		<h:form id="inputForm" enctype="#{cc.attrs.enctype}">
			<composite:insertChildren />
		</h:form>
	</fieldset>
</composite:implementation>



</html>
```

rajouter dans la page xhtml le 

xmlns:etrs="http://java.sun.com/jsf/composite/etrs"