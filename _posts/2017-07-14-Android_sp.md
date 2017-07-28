---
layout: post
title:  "android native"
image: ''
date:   2017-07-20 20:20:25
tags:
- snippet android activity native java
description: 'android'
categories:
- snippets  
---

# Main Activity


**E**s normal que al hacer aplicaciones para terceros uno se consiga con especificaciones de diseño, reuniones con el cliente, precios, etc. Al menos en pequeñas app. Cuando hice la aplicacion para la PCP (Policia Canina Peruana), segui los diseños sugeridos, edite fotos, en fin. Uno da la milla extra y piensa que todo bien. Y la aplicacion se cancela (nueva administracion?). >.> . Para no quedarme con las ganas, agarre algo de ese codigo y lo re-use en una aplicacion de Montaña. AvilaCaracas se llama. Ahora me doy cuenta que es bien comodo que te den los diseños, requerimientos, y "theme". Que fea me salio la app XD. Pero bueno, alli esta, para medir cuanto me demoro en subir al Avila (ya se, es "waraira repano"). Tal vez cuando tenga tiempo integre un ui con animaciones, un calendario y si consigo un "partnership" con alguien, le monte una tienda usando webview. Bueno, como aqui lo que hago es compartir codigo, dejare una parte interesante como lo es la actividad principal que llama a los fragments. Otro codigo interesante es cuando se integra libgdx dentro de un fragment, es algo para juegos mas que todo, bueno, sera para la proxima ^^.

````java

package com.fenix.binary.avilacaracas;

import android.os.Bundle;
import android.support.design.widget.TabLayout;
import android.support.v4.app.Fragment;
import android.support.v4.app.FragmentManager;
import android.support.v4.app.FragmentStatePagerAdapter;
import android.support.v4.view.ViewPager;
import android.support.v7.app.AppCompatActivity;

import java.util.ArrayList;

public class MainActivity extends AppCompatActivity {

    private ViewPager viewPager;
    private TabLayout tabLayout;
    private ViewpagerAdapter viewPagerAdapter;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        viewPager = (ViewPager)findViewById(R.id.toolbar_viewpager);
        create_and_prepare_Adapter();
        viewPager.setAdapter(viewPagerAdapter);
        tabLayout = (TabLayout)findViewById(R.id.toolbar_tabs);
        tabLayout.setupWithViewPager(viewPager);

        tabLayout.addOnTabSelectedListener(new TabLayout.OnTabSelectedListener() {
            @Override
            public void onTabSelected(TabLayout.Tab tab) {
                /*Esta es la parte que esta pendiente de cuando el tab esta seleccionado*/
                viewPager.setCurrentItem(tab.getPosition()); /*el viewpager esta pendiente de las animaciones
                correspondientes al lugar de presionado en el tab*/
            }

            @Override
            public void onTabUnselected(TabLayout.Tab tab) {

            }

            @Override
            public void onTabReselected(TabLayout.Tab tab) {

            }
        });
    }

    private void create_and_prepare_Adapter() {
        viewPagerAdapter = new ViewpagerAdapter(getSupportFragmentManager());// inicializacion general

        viewPagerAdapter.addFragment(new Fg_excursionista(),"Excursionista");
        viewPagerAdapter.addFragment(new Fg_lugares(),"Lugares");
        viewPagerAdapter.addFragment(new Fg_historia(),"Historia");
    }

    private class ViewpagerAdapter extends FragmentStatePagerAdapter{

       private final ArrayList<Fragment> atomic_fragment = new ArrayList<Fragment>();
       private final ArrayList<String> atomic_fragment_titulos = new ArrayList<String>();

        public ViewpagerAdapter(FragmentManager fm) {
            super(fm);
        }

        @Override
        public Fragment getItem(int position) {
            return atomic_fragment.get(position);
        }

        @Override
        public int getCount() {
            return atomic_fragment.size();
        }

        @Override
        public CharSequence getPageTitle(int position) {
            return atomic_fragment_titulos.get(position);
        }
        //init
        public void addFragment(Fragment fragment,String s){
            atomic_fragment.add(fragment);
            atomic_fragment_titulos.add(s);
        }
    }
}

````
