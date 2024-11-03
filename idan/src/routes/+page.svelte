<script>
	import { quintOut } from "svelte/easing";
	import { fly } from "svelte/transition";

    let name = '';
    let phone = '';
    let message = '';
    let showModal = false;
  
    const sendToTelegram = async () => {
      if (!name || !phone ) {
        alert('נא למלא את כל השדות');
      }
      const text = `שם: ${name}\nטלפון: ${phone}\nהודעה: ${message}`;
  
      const response = await fetch(`https://api.telegram.org/bot${import.meta.env.VITE_BOT_ID}/sendMessage`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          chat_id: import.meta.env.VITE_CHAT_ID,
          text
      })
      });
  

      if (response.ok) {
        alert('ההודעה נשלחה בהצלחה!');
      } else {
        alert('שגיאה בשליחת ההודעה.');
      }
    };
  
    const whatsappUrl = `https://wa.me/972522054592?text=שלום, אני מעוניין בשירותי הובלה.`;
    let showForm = false;

    const toggleModal = () => {
        showModal = !showModal;
    };
  </script>
  
  <style>
    :global(body) {
        margin: 0;
        padding: 0;
        min-height: 100vh;
        background-color: #1D4E89;
    }

    .body {
        direction: rtl;
        font-family: Arial, sans-serif;
        background-color: #1D4E89;
        color: white;
        text-align: center;
        padding: 20px;
        min-height: 100vh;
        box-sizing: border-box;
    }
  
    .form-container {
      max-width: 400px;
      margin: 0 auto;
      padding: 20px;
      background-color: #254EA5; /* גוון כחול כהה */
      border-radius: 8px;
      box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.2);
    }
  
    label {
      display: block;
      margin-bottom: 8px;
      font-weight: bold;
    }
  
    input, textarea {
      width: 100%;
      padding: 8px;
      margin-bottom: 16px;
      border-radius: 4px;
      border: none;
      color:#1D4E89 ;
      border: 1px solid #DDD;
    }
  
    .button {
      width: 100%;
      padding: 10px;
      background-image: linear-gradient(45deg, #FFD700, #FFA500); /* מעבר גוונים */
      color: white;
      border: none;
      border-radius: 4px;
      font-size: 16px;
      cursor: pointer;
    }
  
    .whatsapp-button {
      display: inline-block;
      margin-top: 20px;
      padding: 10px 20px;
      color: #FFD700;
      background-color: transparent;
      border: 2px solid #FFD700;
      border-radius: 4px;
      text-decoration: none;
      font-size: 16px;
      transition: 0.3s;
    }
  
    .whatsapp-button:hover {
      background-color: #FFD700;
      color: #1D4E89;
    }
       /* הוספת עיצוב לרשימת השירותים */
       .services-section {
      margin-top: 20px;
      padding: 20px;
      background-color: #254EA5; /* גוון כחול כהה */
      border-radius: 8px;
      color: white;
    }
  
    .services-section h2 {
      font-size: 24px;
      margin-bottom: 16px;
      color: #FFD700; /* זהב */
    }
  
    .service-item {
      margin-bottom: 12px;
      padding-left: 10px;
      position: relative;
    }
  
    .service-item:before {
      content: '✔';
      position: absolute;
      right: 0;
      color: #FFD700;
      font-size: 16px;
    }
  
    .service-description {
      font-size: 14px;
      color: #DDD;
    }
    h1 {
  color:#ffffff;
  font-family:Verdana, Geneva, Tahoma, sans-serif;
  text-align: center;
}
li{
    font-size: 20px;
}
.rainbow-btn {
    width: fit-content;
    text-align: center;
    position: relative;
    color: #ffffff;
    text-decoration: none;
    border-radius: 6px;
    box-sizing: border-box;
    display: block;
    z-index: 2;
    overflow: hidden;
    padding: 8px;
    margin: 0 auto; 
}
.rainbow-btn:before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 200%;
    height: 100%;
    background: linear-gradient(115deg,#4fcf70,#fad648,#a767e5,#12bcfe,#44ce7b);
    background-size: 50% 100%
}
.rainbow-btn span {
    position: relative;
    z-index: 2;
    padding: .875rem 1rem;
    font-size: 1.1rem;
    text-decoration: none;
    align-items: center;
    background: #000;
    border-radius: 3px;
    display: block;
    justify-content: center;
    box-sizing: border-box;
    height: 100%;
    font-family:Verdana, Geneva, Tahoma, sans-serif;
}
.rainbow-btn:before,
.rainbow-btn:before {
    animation: rainbow-btn .75s linear infinite
}
.rainbow-btn:focus:before,
.rainbow-btn:hover:before {
    animation: rainbow-btn 1.75s linear infinite
}

@keyframes rainbow-btn {
    to {
        transform: translateX(-50%)
    }
}

.logo-image {
  max-width: 200px; /* או כל גודל אחר שתרצה */
  height: auto;
  margin: 0 auto;
  display: block;
  margin-bottom: 20px;
  border-radius: 10px; /* אם תרצה פינות מעוגלות */
}

.modal {
  z-index: 9999;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    transition: opacity 0.3s ease;
}


.modal-content {
    background-color: #254EA5; /* גוון כחול כהה */
    padding: 30px;
    border-radius: 8px;
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.2);
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;    
}
label{
  font-size: 15px;
  color: #FFD700;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}

  </style>
  <div class="body">

   
  <!-- קטע שירותי החברה -->
  <div class=" rainbow-btn " dir="rtl">
    <span>
      <img src="/logoIdan.jpg" alt="עידן הובלות לוגו" class="logo-image" />
      <h1>עידן הובלות</h1>
      <p class="text-xl">שירותי הובלה מקצועיים בטבריה ובכל הארץ</p>
    <ul>
      <li class="service-item">
        הובלות דירות
        <p class="service-description">הובלת דירות בצורה מקצועית, מהירה ובטוחה.</p>
      </li>
      <li class="service-item">
        הובלות משרדים
        <p class="service-description">שירותי העברת משרדים תוך שמירה על רהיטים וציוד משרדי.</p>
      </li>
      <li class="service-item">
        שירותי מנוף
        <p class="service-description">שירותי מנוף להעברת פריטים גדולים לקומות גבוהות.</p>
      </li>
      <li class="service-item">
        שירותי אחסון
        <p class="service-description">פתרונות אחסון זמניים ובטוחים לתכולה.</p>
      </li>
      <li class="service-item">
        שירותי פירוק והרכבה
        <p class="service-description">פירוק והרכבה מקצועית של רהיטים להעברה קלה יותר.</p>
      </li>
      <li class="service-item">
        הובלות קטנות לכל הארץ
        <p class="service-description">שירותי הובלה קטנים ונוחים לכל יעד בארץ.</p>
      </li>
    </ul>
</span>
  </div>

  <a class="whatsapp-button" href={whatsappUrl} target="_blank">צרו קשר ב-WhatsApp</a>
  {#if !showModal}
  <button class="whatsapp-button" onclick={toggleModal}>השארת פרטים</button>
  {/if}
 </div>
 {#if showModal}
 <div class="modal flex flex-row items-center justify-center p-5" transition:fly="{{delay: 250, duration: 300, x: 100, y: 500, opacity: 0.5, easing: quintOut}}">
       <div class="modal-content">
  <button class="text-white p-2 bg-gold rounded-full" onclick={toggleModal}>סגירה</button>
         <label>שם</label>
         <input type="text" class="text-pink-700" bind:value={name} placeholder=" שם מלא" />
     
         <label>טלפון</label>
         <input type="tel" bind:value={phone} placeholder=" מספר טלפון" />
     
         <label>הודעה</label>
         <textarea bind:value={message} placeholder=" הודעה"></textarea>
     
         <button class="button bg-transparent" onclick={sendToTelegram}>צרו איתי קשר</button>
        </div>
        </div>
 {/if}