# Converter (FacesConverter)

Transforme les String reçus depuis le web en Objets exploitables par Java.
Et inversement.

``` java
package haribo4ever.converters;

import javax.enterprise.context.ApplicationScoped;
import javax.faces.component.UIComponent;
import javax.faces.context.FacesContext;
import javax.faces.convert.Converter;
import javax.faces.convert.FacesConverter;
import javax.inject.Inject;

import haribo4ever.model.dao.DaoPaquet;
import haribo4ever.model.entities.Paquet;

@ApplicationScoped
@FacesConverter(forClass = Paquet.class)
public class PaquetConverter implements Converter {

	@Inject
	private DaoPaquet dao;

	@Override
	public Object getAsObject(FacesContext ctx, UIComponent cmp, String value) {

		return (value == null) ? null : dao.read(value);
	}

	@Override
	public String getAsString(FacesContext ctx, UIComponent cmp, Object o) {
		return (o instanceof Paquet) ? ((Paquet) o).getId() : null;
	}

}
```

## le GenericConverter
```

<h:selectManyCheckbox 
	id="selectCompetences"
	value="#{modifierPersonneBean.personne.competences}"
	converter="#{genericConverter}"
	class="form-check">
		<f:selectItems value="#{modifierPersonneBean.listeCompetences}"
			var="c" itemLabel="#{c.libelle}" itemValue="#{c}" />
</h:selectManyCheckbox>

```