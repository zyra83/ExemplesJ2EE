Utiliser le flashScope avec le converterPaquet


mettre le paquet en falsh scope
Page listerPaquetFalshScope

variable a faire
public static final String FLASH_PARAM_PAQUET = "paquet_selectionne";

public void mettrePaquetEnFlashScope(Paquet paquetSelectionne){
	JsfUtils.putInFlashScope(FLASH_PARAM_PAQUET, paquetSelectionne);
}

Page afficherPaquetFalshScope

@SuppressWarnings("serial")
@Named
@ViewScoped // reste la même vue tant qu'il y a des probelems de saisie pour l'utilisateur
public class AffichePaquetFlashScopePageBean implements Serializable {

	@Getter
	@Setter
	private Paquet paquet;
	
	@PostConstruct
	public void init(){
		paquet = (Paquet) JsfUtils.getFromFlashScope(ListerPaquetsFlashScopePageBean.FLASH_PARAM_PAQUET);
	}

}

Pas besoin du converter
si on utilise  pas de scope

Page listerPaquet

<h:link value="#{p.nom}" outcome="afficher-paquet.xhtml">
	<f:param name="uuid" value="#{p.id}" />
</h:link>


Page afficherPaquet.xhttml

<f:metadata>
	<f:viewParam name="uuid" value="#{affichePaquetBean.paquet}"
		converter="#{paquetConverter}" />
</f:metadata>


Bean

@SuppressWarnings("serial")
@Named
@ViewScoped // reste la même vue tant qu'il y a des probelems de saisie pour
			// l'utilisateur
@ManagedBean
public class AffichePaquetBean implements Serializable {

	@Getter
	@Setter
	String uuid;

	@Getter
	@Setter
	private Paquet paquet;

}