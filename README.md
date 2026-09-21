igreja.java

package com.example.igrejaapi;

public class Igreja {
    private String nome;
    private String cidade;
    private String endereco;
    private String pix;
    private String whatsapp;

    public String getNome(){

        return nome;
    }
    public void setNome(String nome)
    {
        this.nome= nome;
    }
    public String getCidade()
    {
      return cidade;
    }

    public void setCidade(String cidade){

        this.cidade=cidade;
    }
    public String getEndereco(){

        return endereco;
    }
    public void setEndereco(String endereco)
    {
        this.endereco=endereco;
    }

    public String getPix(){

        return pix;
    }
    public void setPix(String pix){

        this.pix=pix;
    }
    public String getWhatsapp(){
        return whatsapp;
    }
    public void setWhatsapp(String whatsapp){
        this.whatsapp= whatsapp;
    }

}






//controllerigreja


package com.example.igrejaapi;


import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class IgrejaController {

    @GetMapping("/igreja")
    public Igreja igreja(){

        Igreja dados = new Igreja();

        dados.setNome("Igreja Videira Formosa");
        dados.setCidade("Formosa");
        dados.setEndereco("Avenida cristalina, setor sul");
        dados.setPix("13.571.038/0001-66");
        dados.setWhatsapp("(61) 9814-8641");

         return dados;

    }
}




// evento.java




package com.example.igrejaapi;

public class Evento {

    private String nome;
    private String data;
    private String local;
    private int id;

    public String getNome(){
        return nome;
    }
    public void setNome(String nome){
        this.nome=nome;
    }
    public String getData()
    {return data;}

    public void setData(String data)
    {this.data=data;}

    public String getLocal()
    {return local;}

    public void setLocal(String local){

        this.local=local;
    }
    public int getId()
    {
        return id;
    }

    public void setId(int id)
    {
        this.id=id;
    }
}






// controllereventos




package com.example.igrejaapi;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.server.ResponseStatusException;
import org.springframework.http.HttpStatus;

import java.util.ArrayList;
import java.util.List;

@RestController
public class Eventocontroller {

    private List<Evento> eventos = new ArrayList<>();
    private int proximoId = 1;

    @GetMapping("/eventos")
    public List<Evento> eventos() {
        return eventos;
    }

    @GetMapping("/eventos/{id}")
    public Evento buscarEvento(@PathVariable int id) {

        for (Evento evento : eventos) {
            if (evento.getId() == id) {
                return evento;
            }
        }

        throw new ResponseStatusException(
                HttpStatus.NOT_FOUND,
                "Evento não encontrado"
        );
    }

    @DeleteMapping("/eventos/{id}")
    public void excluirEvento(@PathVariable int id) {

        eventos.removeIf(evento -> evento.getId() == id);
    }

    @PostMapping("/eventos")
    public Evento cadastrarevento(@RequestBody Evento evento) {

        evento.setId(proximoId);
        proximoId++;

        eventos.add(evento);
        return evento;
    }

    @PutMapping("/eventos/{id}")
    public Evento editarEvento(@PathVariable int id, @RequestBody Evento novoEvento) {

        for (Evento evento : eventos) {

            if (evento.getId() == id) {

                evento.setNome(novoEvento.getNome());
                evento.setData(novoEvento.getData());
                evento.setLocal(novoEvento.getLocal());

                return evento;
            }
        }

        throw new ResponseStatusException(
                HttpStatus.NOT_FOUND,
                "Evento não encontrado"
        );
    }
}





//celula.java






package com.example.igrejaapi;

public class Celula {
    private String nome;
    private String dia;
    private String horario;
    private String local;
    private int Id;


    public String getNome()
    {
        return nome;
    }
    public void setNome(String nome)
    {
        this.nome=nome;
    }
    public String getDia()
    {
        return dia;
    }
    public void setDia(String dia)
    {
        this.dia=dia;
    }
    public String getHorario()
    {
        return  horario;
    }
    public void setHorario(String horario)
    {
        this.horario=horario;
    }
    public String getLocal()
    {
        return  local;
    }
    public  void  setLocal(String local)
    {
        this.local=local;
    }
    public int getId(){
        return Id;
    }
    public void setId(int id) {
        this.Id = id;
    }
}





//celulacontroller



package com.example.igrejaapi;

import java.util.ArrayList;
import java.util.List;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.server.ResponseStatusException;
import org.springframework.http.HttpStatus;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.PutMapping;

@RestController
public class Celulacontroller {

    private List<Celula> celulas = new ArrayList<>();
    private int proximoId = 1;

    @GetMapping("/celulas")
    public List<Celula> celulas() {
        return celulas;
    }

    @GetMapping("/celulas/{id}")
    public Celula buscarCelula(@PathVariable int id) {

        for (Celula celula : celulas) {
            if (celula.getId() == id) {
                return celula;
            }
        }

        throw new ResponseStatusException(
                HttpStatus.NOT_FOUND,
                "Célula não encontrada"
        );
    }

    @PostMapping("/celulas")
    public Celula cadastrarCelula(@RequestBody Celula celula) {
        celula.setId(proximoId);
        proximoId++;

        celulas.add(celula);
        return celula;
    }

    @DeleteMapping("/celulas/{id}")
    public void excluirCelula(@PathVariable int id){

        celulas.removeIf(celula -> celula.getId() == id);

        //“Na lista celulas, remova a celula cujo id seja igual ao id recebido na URL.”
    }


    @PutMapping("/celulas/{id}")
    public Celula editarCelula(@PathVariable int id, @RequestBody Celula novacelula){
        for (Celula celula: celulas){
            if (celula.getId()== id){



                celula.setNome(novacelula.getNome());
                celula.setDia(novacelula.getDia());
                celula.setHorario(novacelula.getHorario());
                celula.setLocal(novacelula.getLocal());

                return celula;
            }
        }

        throw new ResponseStatusException(
                HttpStatus.NOT_FOUND,
                "Célula não encontrada"
        );
    }



}






//celulakids.java



package com.example.igrejaapi;

import java.util.ArrayList;
import java.util.List;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.server.ResponseStatusException;
import org.springframework.http.HttpStatus;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.PutMapping;

@RestController
public class Celulacontroller {

    private List<Celula> celulas = new ArrayList<>();
    private int proximoId = 1;

    @GetMapping("/celulas")
    public List<Celula> celulas() {
        return celulas;
    }

    @GetMapping("/celulas/{id}")
    public Celula buscarCelula(@PathVariable int id) {

        for (Celula celula : celulas) {
            if (celula.getId() == id) {
                return celula;
            }
        }

        throw new ResponseStatusException(
                HttpStatus.NOT_FOUND,
                "Célula não encontrada"
        );
    }

    @PostMapping("/celulas")
    public Celula cadastrarCelula(@RequestBody Celula celula) {
        celula.setId(proximoId);
        proximoId++;

        celulas.add(celula);
        return celula;
    }

    @DeleteMapping("/celulas/{id}")
    public void excluirCelula(@PathVariable int id){

        celulas.removeIf(celula -> celula.getId() == id);

        //“Na lista celulas, remova a celula cujo id seja igual ao id recebido na URL.”
    }


    @PutMapping("/celulas/{id}")
    public Celula editarCelula(@PathVariable int id, @RequestBody Celula novacelula){
        for (Celula celula: celulas){
            if (celula.getId()== id){



                celula.setNome(novacelula.getNome());
                celula.setDia(novacelula.getDia());
                celula.setHorario(novacelula.getHorario());
                celula.setLocal(novacelula.getLocal());

                return celula;
            }
        }

        throw new ResponseStatusException(
                HttpStatus.NOT_FOUND,
                "Célula não encontrada"
        );
    }



}




//celulakidacontroller




package com.example.igrejaapi;

import org.springframework.web.bind.annotation.*;
import java.util.List;
import java.util.ArrayList;
import org.springframework.web.server.ResponseStatusException;
import org.springframework.http.HttpStatus;

    @RestController
    public class Celulakidscontroller {

        private List<Celulakids> celulaskids = new ArrayList<>();

        @GetMapping("/celulaskids")
        public List<Celulakids> celulaskids() {
            return celulaskids;
        }

        @GetMapping("/celulaskids/{id}")
        public Celulakids buscarCelulakids(@PathVariable int id) {

            for (Celulakids celulakids : celulaskids) {
                if (celulakids.getId() == id) {
                    return celulakids;
                }
            }


            throw new ResponseStatusException(
                    HttpStatus.NOT_FOUND,
                    "Célula Kids não encontrada"
            );
        }

        private int proximoId = 1;

        @PostMapping("/celulaskids")
        public Celulakids cadastrarCelulaKids(@RequestBody Celulakids celulaKids) {

            celulaKids.setId(proximoId);
            proximoId++;

            celulaskids.add(celulaKids);

            return celulaKids;

        }

        @DeleteMapping("/celulaskids/{id}")
        public void excluirCelulakids(@PathVariable int id) {

            celulaskids.removeIf(celulakids -> celulakids.getId() == id);


        }

        @PutMapping("/celulaskids/{id}")
        public Celulakids editarCelulakids(@PathVariable int id, @RequestBody Celulakids novacelulakids) {
            for (Celulakids celulakids : celulaskids) {
                if (celulakids.getId() == id) {


                    celulakids.setNome(novacelulakids.getNome());
                    celulakids.setDia(novacelulakids.getDia());
                    celulakids.setHorario(novacelulakids.getHorario());
                    celulakids.setLocal(novacelulakids.getLocal());

                    return celulakids;
                }
            }

            throw new ResponseStatusException(
                    HttpStatus.NOT_FOUND,
                    "Célula Kids não encontrada"
            );


        }

    }




    //visitantejava



    package com.example.igrejaapi;

public class Visitante {

    private String nome;
    private String telefone;
    private String cidade;
    private int id;

    public String getNome(){
        return nome;

    }
    public void setNome(String nome){
        this.nome=nome;

    }
    public String getTelefone(){
    return telefone;
    }
    public void setTelefone(String telefone){
        this.telefone=telefone;

    }
    public String getCidade()
    {
        return cidade;
    }
    public void setCidade(String cidade)
    {
        this.cidade=cidade;

    }
    public int getId(){
        return id;

    }
    public void setId(int id){
        this.id=id;
    }




}



// visitantecontroller




package com.example.igrejaapi;

import org.springframework.web.bind.annotation.*;

        import java.util.ArrayList;
import java.util.List;
import org.springframework.web.server.ResponseStatusException;
import org.springframework.http.HttpStatus;

@RestController
public class Visitantecontroller {

    private List<Visitante> visitantes = new ArrayList<>();

    private int proximoId = 1;

    @GetMapping("/visitantes")
    public List<Visitante> visitantes() {

        return visitantes;
    }

    @GetMapping("/visitantes/{id}")
    public Visitante buscarVisitante(@PathVariable int id) {

        for (Visitante visitante : visitantes) {
            if (visitante.getId() == id) {
                return visitante;
            }
        }
        throw new ResponseStatusException(
                HttpStatus.NOT_FOUND,
                "Visitante não encontrado"
        );
    }

    @PostMapping("/visitantes")
    public Visitante cadastrarVisitante(@RequestBody Visitante visitante) {

        visitante.setId(proximoId);
        proximoId++;

        visitantes.add(visitante);

        return visitante;

    }

    @DeleteMapping("/visitantes/{id}")
    public void excluirVisitante(@PathVariable int id) {

        visitantes.removeIf(visitante -> visitante.getId() == id);
    }

    @PutMapping("/visitantes/{id}")
    public Visitante editarVisitante(@PathVariable int id, @RequestBody Visitante novoVisitante) {

        for (Visitante visitante : visitantes) {

            if (visitante.getId() == id) {

                visitante.setNome(novoVisitante.getNome());
                visitante.setTelefone(novoVisitante.getTelefone());
                visitante.setCidade(novoVisitante.getCidade());

                return visitante;
            }
        }
        throw new ResponseStatusException(
                HttpStatus.NOT_FOUND,
                "Visitante não encontrado"
        );
    }
}





