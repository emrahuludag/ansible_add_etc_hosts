#Inventory Dosyasındaki Host'ları Tum Node'lardaki Hosts Dosyasına Ekleme

>---
- hosts: allnode
  become: yes
  tasks:

   - name: Add IP address of all hosts to all hosts
     lineinfile:
      dest: /etc/hosts
      regexp: '.*{{ item }}$'
      line: "{{ hostvars[item].ansible_host }} {{item}}"
      state: present
     when: hostvars[item].ansible_host is defined
     with_items: "{{ groups.all }}"

