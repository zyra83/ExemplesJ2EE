# Webservice SOAP

- Créer une classe dans com.appwhite.interop
- annoter la classe :
	- @Stateless
	- @WebService(name="SkillInterop", serviceName="SkillService")
		- name : nom de la classe en anglais ! NAME FAIT DISPARAITRE DE PAYARA !
		- serviceName : nom du service en anglais
	- @SOAPBinding(style=Style.DOCUMENT)
- injecter la façade nécessaire 
- créer la méthode à mettre à disposition dans le service
	- @WebMethod(operationName="listSkills")
		- nommer la méthode en anlgais
    - @XmlElement(name="skill")
		- nommer les retours en anglais
		- ne pas placer sur les méthodes void
	- nommer les paramètres de la méthode en anglais
		- @WebParam(name="title")



``` java
package com.appwhite.interop;

import java.util.List;

import javax.ejb.Stateless;
import javax.inject.Inject;
import javax.jws.WebMethod;
import javax.jws.WebParam;
import javax.jws.WebService;
import javax.jws.soap.SOAPBinding;
import javax.jws.soap.SOAPBinding.Style;
import javax.xml.bind.annotation.XmlElement;
import javax.xml.soap.SOAPException;

import com.appwhite.model.entities.annuaire.Competence;
import com.appwhite.model.sessions.annuaire.FacadeCompetence;

@Stateless
@WebService(name="SkillInterop", serviceName="SkillService")
@SOAPBinding(style=Style.DOCUMENT)
public class CompetenceInterop {
	
	@Inject
	private FacadeCompetence facade;
	
	@WebMethod(operationName="listSkills")
	@XmlElement(name="skill")
	public List <Competence> listerCompetences() throws SOAPException
	{
		// retourne la liste des compétences triées sur le libellé.
		return facade.readAll("libelle");
		
		// exemple de déclenchement d'une erreur SOAP
		// throw new SOAPException("Pas de chance");
	}
	
	@WebMethod(operationName="addSkill")
	public void ajouterCompetence(@WebParam(name="title") String libelle, 
								  @WebParam(name="details") String description)
	{
		Competence c = facade.newInstance(libelle, description);
		facade.create(c);
	}

}
```