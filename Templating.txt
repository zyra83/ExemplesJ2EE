# Templating

## Au niveau des fragments
Définir des fragments à inclure dans les templates.
Ils ont aussi des zones d'insertion.

``` html
<ui:fragment xmlns="http://www.w3.org/1999/xhtml"
	xmlns:h="http://java.sun.com/jsf/html"
	xmlns:f="http://java.sun.com/jsf/core"
	xmlns:ui="http://java.sun.com/jsf/facelets"
	xmlns:p="http://primefaces.org/ui">

	<footer class="footer">
		<div class="container">
			<p class="text-muted">
				<h:outputText value="#{msg['template.bas-de-page']}" escape="false" />
			</p>
		</div>
	</footer>

	<p:growl globalOnly="true" autoUpdate="true" />


	<!-- Nécessaire pour BootStrap -->
	<h:outputScript library="primefaces" name="jquery/jquery.js"
		target="head" />
	<h:outputScript library="primefaces" name="jquery/jquery-plugins.js"
		target="head" />
	<h:outputScript name="bootstrap/js/bootstrap.min.js" />
	
</ui:fragment>
```
## Au niveau des pages template

	WebContent/META-INF/templates/standard.xhtml

Définir une zone à insérer depuis les pages

	<ui:insert name="content">Votre contenu...</ui:insert>

Pour charger des fragments
	
	<ui:include src="/WEB-INF/templates/fragments/fragment-bootstrap-nav.xhtml" />

## Au niveau des pages clientes
Pour aller écrire dans une zone du template
- > /AppWhiteSingleWar/WebContent/competence/creer-competence.xhtml

	<ui:define name="title">Compétences - créer une compétence</ui:define>