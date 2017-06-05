# Servlet

- assistant Servlet > nouvelle
	- package com.appwhite.servlets
	- nom qui finit par Servlet
	- url mapping (nom tirets sans majuscules)  :  /serve-paquet-image
	- ne laisser que le doGet()

``` java

package servlets;

import java.io.IOException;

import javax.enterprise.inject.Instance;
import javax.inject.Inject;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import haribo4ever.model.dao.DaoPaquetJPA;
import haribo4ever.model.entities.Paquet;

/**
 * Servlet implementation class ServePaquetImageServlet
 */
@WebServlet("/serve-paquet-image")
public class ServePaquetImageServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

	@Inject
	Instance<DaoPaquetJPA> instance;

	@Inject
	private DaoPaquetJPA dao;

	/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse
	 *      response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		DaoPaquetJPA dao = instance.get();
		// /server-paquet-image?id=450-3456-aze
		//http://vmprog:8080/HariboForEver/serve-paquet-image?id=19d75189-bfca-4214-ad69-98f642627097

		String id = request.getParameter("id");
		if (id != null) {
			//

			Paquet p = dao.read(id);
			if (p != null && p.getImage() != null) {
				byte[] img = p.getImage();
				response.setContentType("image/jpeg");
				response.getOutputStream().write(img);
				response.flushBuffer();
			} else {
				// retourner 404
				response.sendError(HttpServletResponse.SC_NOT_FOUND, "image ou identifiant incorrect");
			}
		} else {
			// retourner 404
			response.sendError(HttpServletResponse.SC_NOT_FOUND, "image ou identifiant incorrect");
		}

	}

}
```