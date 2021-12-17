---
title: 팀 소개
feature_text: |
  ### 우리는 백엔드 개발팀, <span style="color:#1EB563">비상사태</span>입니다!
  견고한 시스템을 구축하여 어떤 **비상사태**도 함께 잘 해쳐나가자는 의미를 담고있어요.💪
feature_image: "https://images.unsplash.com/photo-1518655048521-f130df041f66?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80"
excerpt: 팀 소개
---

<div class="about">
    <div class="section">
        <div class="group-wrapper">
            <div class="group">
                <div class="group-name">#대장 #리더</div>
                <ul class="member">
                    {% assign members = site.data.members | where: 'group', 'leader' | where_exp: 'member', 'member.drop != true' | sort: 'id' %}
                    {% for member in members %}
                        {% include about-member.html %}
                    {% endfor %}
                </ul>
            </div>
            <div class="group">
                <div class="group-name">#인프라</div>
                <ul class="member">
                    {% assign members = site.data.members | where: 'group', 'infra' | where_exp: 'member', 'member.drop != true' | sort: 'id' %}
                    {% for member in members %}
                        {% include about-member.html %}
                    {% endfor %}
                </ul>
            </div>
            <div class="group">
                <div class="group-name">#기획자</div>
                <ul class="member">
                    {% assign members = site.data.members | where: 'group', 'planner' | where_exp: 'member', 'member.drop != true' | sort: 'id' %}
                    {% for member in members %}
                        {% include about-member.html %}
                    {% endfor %}
                </ul>
            </div>
            <div class="group">
                <div class="group-name">#백엔드</div>
                <ul class="member">
                    {% assign members = site.data.members | where: 'group', 'backend' | where_exp: 'member', 'member.drop != true' | sort: 'id' %}
                    {% for member in members %}
                        {% include about-member.html %}
                    {% endfor %}
                </ul>
            </div>
        </div>
    </div>
</div>