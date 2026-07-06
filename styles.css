const chatToggle = document.querySelector(".chat-toggle");
const chatBox = document.querySelector(".chat-box");
const chatClose = document.querySelector(".chat-close");
const chatForm = document.querySelector(".chat-form");
const chatMessage = document.querySelector("#chatMessage");
const quickMessages = document.querySelectorAll(".quick-messages button");
const eventForm = document.querySelector("#eventForm");
const feedbackForm = document.querySelector("#feedbackForm");
const weeklyMenuView = document.querySelector("#weeklyMenuView");
const eventCalendarView = document.querySelector("#eventCalendarView");
const coffeeMenuList = document.querySelector("#coffeeMenuList");
const kitchenMenuList = document.querySelector("#kitchenMenuList");

const restaurantWhatsAppNumber = "358407557155";
const restaurantEmail = "ravintola@paatelanportti.com";
const weeklyMenuFile = "weekly-menu.json";
const eventCalendarFile = "events-calendar.json";
const foodMenuFile = "food-menu.json";
const siteImagesFile = "site-images.json";

const defaultWeeklyMenu = [
  "Maanantai: Makkarakeittoa, leipää, ruokajuomat",
  "Tiistai: Jauhelihakeittoa, leipää, ruokajuomat",
  "Keskiviikko: Kasvissosekeittoa, leipää, ruokajuomat",
  "Torstai: Hernekeittoa, leipää, ruokajuomat, pannari tai jäätelö",
  "Perjantai: Lohikeittoa, leivät, ruokajuomat",
  "Lauantai: Savuporo-juustokeittoa, leivät, ruokajuomat"
].join("\n");

const defaultEventCalendar = [
  "Torstaisin | klo 18.00 | Kanavakaraoke | Vetäjänä tuttu Timo Kolu.",
  "Perjantaisin | klo 20.00 | Karaoke | Karaoken tuottaa AJ Viihde.",
  "Lauantaisin | illalla | Tanssi-iltoja ja elävää musiikkia | Viikonlopun esiintyjät ja ohjelma päivitetään tähän tarpeen mukaan."
].join("\n");

function setChatOpen(isOpen) {
  if (!chatBox || !chatToggle || !chatMessage) return;

  chatBox.hidden = !isOpen;
  chatToggle.setAttribute("aria-expanded", String(isOpen));

  if (isOpen) {
    chatMessage.focus();
  }
}

if (chatToggle && chatBox) {
  chatToggle.addEventListener("click", () => {
    setChatOpen(chatBox.hidden);
  });
}

if (chatClose) {
  chatClose.addEventListener("click", () => {
    setChatOpen(false);
  });
}

quickMessages.forEach((button) => {
  button.addEventListener("click", () => {
    if (!chatMessage) return;
    chatMessage.value = button.dataset.message || "";
    chatMessage.focus();
  });
});

function renderWeeklyMenu(text) {
  if (!weeklyMenuView) return;

  const lines = text
    .split("\n")
    .map((line) => line.trim())
    .filter(Boolean);

  weeklyMenuView.replaceChildren();

  lines.forEach((line) => {
    const [day, ...rest] = line.split(":");
    const menu = rest.join(":").trim() || "Päivitetään pian";
    const item = document.createElement("div");
    const title = document.createElement("strong");
    const body = document.createElement("span");

    item.className = "weekly-day";
    title.textContent = day.trim();
    body.textContent = menu;
    item.append(title, body);
    weeklyMenuView.append(item);
  });
}

function weeklyItemsToText(items) {
  return items.map((item) => `${item.day}: ${item.menu}`).join("\n");
}

function renderEventCalendar(text) {
  if (!eventCalendarView) return;

  const lines = text
    .split("\n")
    .map((line) => line.trim())
    .filter(Boolean);

  eventCalendarView.replaceChildren();

  lines.forEach((line) => {
    const [day = "", time = "", title = "", description = ""] = line
      .split("|")
      .map((part) => part.trim());
    const item = document.createElement("article");
    const meta = document.createElement("div");
    const dayElement = document.createElement("strong");
    const timeElement = document.createElement("span");
    const content = document.createElement("div");
    const titleElement = document.createElement("h4");
    const descriptionElement = document.createElement("p");

    item.className = "event-calendar-item";
    meta.className = "event-calendar-meta";
    content.className = "event-calendar-content";

    dayElement.textContent = day || "Päivä";
    timeElement.textContent = time || "Aika tarkentuu";
    titleElement.textContent = title || "Tapahtuma";
    descriptionElement.textContent = description || "Lisätiedot päivitetään pian.";

    meta.append(dayElement, timeElement);
    content.append(titleElement, descriptionElement);
    item.append(meta, content);
    eventCalendarView.append(item);
  });
}

function eventItemsToText(items) {
  return items
    .map((item) => `${item.day} | ${item.time} | ${item.title} | ${item.description}`)
    .join("\n");
}

function renderFoodMenuSection(listElement, section) {
  if (!listElement || !section || !Array.isArray(section.items)) return;

  listElement.replaceChildren();

  section.items.forEach((item) => {
    const listItem = document.createElement("li");
    const name = document.createElement("span");

    name.textContent = item.name || "";

    if (item.type === "heading") {
      listItem.className = "price-subheading";
      listItem.append(name);
      listElement.append(listItem);
      return;
    }

    const price = document.createElement("strong");

    price.textContent = item.price || "";
    listItem.append(name, price);
    listElement.append(listItem);
  });
}

function normalizeImagePath(src) {
  if (!src) return "";
  if (src.startsWith("http") || src.startsWith("/")) return src;
  return src;
}

function applySiteImage(image) {
  if (!image || !image.key || !image.src) return;

  const element = document.querySelector(`[data-image-key="${image.key}"]`);
  if (!element) return;

  const src = normalizeImagePath(image.src);

  if (element.tagName.toLowerCase() === "img") {
    element.setAttribute("src", src);
    if (image.alt) {
      element.setAttribute("alt", image.alt);
    }
  } else {
    element.style.backgroundImage = `url("${src}")`;
    if (image.alt) {
      element.setAttribute("aria-label", image.alt);
    }
  }

  if (typeof image.caption === "string") {
    const figure = element.closest("figure");
    const caption = figure ? figure.querySelector("figcaption") : null;
    if (caption) {
      caption.textContent = image.caption;
    }
  }
}

function encodeFormData(form) {
  return new URLSearchParams(new FormData(form)).toString();
}

async function submitNetlifyForm(form) {
  const response = await fetch("/", {
    method: "POST",
    headers: { "Content-Type": "application/x-www-form-urlencoded" },
    body: encodeFormData(form)
  });

  if (!response.ok) {
    throw new Error("Netlify form submit failed");
  }

  window.location.href = form.getAttribute("action") || "/kiitos.html";
}

async function loadWeeklyMenu() {
  try {
    const response = await fetch(weeklyMenuFile, { cache: "no-store" });
    if (!response.ok) {
      throw new Error("weekly menu not available");
    }

    const data = await response.json();
    if (!Array.isArray(data.items)) {
      throw new Error("weekly menu items missing");
    }

    renderWeeklyMenu(weeklyItemsToText(data.items));
  } catch {
    renderWeeklyMenu(defaultWeeklyMenu);
  }
}

async function loadEventCalendar() {
  try {
    const response = await fetch(eventCalendarFile, { cache: "no-store" });
    if (!response.ok) {
      throw new Error("event calendar not available");
    }

    const data = await response.json();
    if (!Array.isArray(data.items)) {
      throw new Error("event calendar items missing");
    }

    renderEventCalendar(eventItemsToText(data.items));
  } catch {
    renderEventCalendar(defaultEventCalendar);
  }
}

async function loadFoodMenu() {
  try {
    const response = await fetch(foodMenuFile, { cache: "no-store" });
    if (!response.ok) {
      throw new Error("food menu not available");
    }

    const data = await response.json();
    if (!Array.isArray(data.sections)) {
      throw new Error("food menu sections missing");
    }

    const coffeeSection = data.sections.find((section) => section.id === "coffee");
    const kitchenSection = data.sections.find((section) => section.id === "kitchen");

    renderFoodMenuSection(coffeeMenuList, coffeeSection);
    renderFoodMenuSection(kitchenMenuList, kitchenSection);
  } catch {
    // The static HTML list is kept as a fallback if the editable file is unavailable.
  }
}

async function loadSiteImages() {
  try {
    const response = await fetch(siteImagesFile, { cache: "no-store" });
    if (!response.ok) {
      throw new Error("site images not available");
    }

    const data = await response.json();
    if (!Array.isArray(data.images)) {
      throw new Error("site image items missing");
    }

    data.images.forEach(applySiteImage);
  } catch {
    // The HTML image paths are kept as a fallback if the editable file is unavailable.
  }
}

if (weeklyMenuView) {
  loadWeeklyMenu();
}

if (eventCalendarView) {
  loadEventCalendar();
}

if (coffeeMenuList || kitchenMenuList) {
  loadFoodMenu();
}

loadSiteImages();

if (eventForm) {
  eventForm.addEventListener("submit", async (event) => {
    event.preventDefault();

    const isLocalPreview = window.location.protocol === "file:";
    const formData = new FormData(eventForm);

    if (!isLocalPreview) {
      try {
        await submitNetlifyForm(eventForm);
      } catch {
        alert("Lähetys ei onnistunut juuri nyt. Voit lähettää tarjouspyynnön myös sähköpostilla: ravintola@paatelanportti.com");
      }
      return;
    }

    const name = formData.get("name") || "";
    const email = formData.get("email") || "";
    const phone = formData.get("phone") || "";
    const date = formData.get("date") || "";
    const eventType = formData.get("eventType") || "";
    const guests = formData.get("guests") || "";
    const message = formData.get("message") || "";

    const subject = `Tarjouspyyntö: ${eventType}`;
    const body = [
      "Hei Paatelan Portti!",
      "",
      "Haluaisin pyytää tarjouksen tilaisuudesta.",
      "",
      `Nimi: ${name}`,
      `Sähköposti: ${email}`,
      `Puhelin: ${phone}`,
      `Tilaisuuden tyyppi: ${eventType}`,
      `Ajankohta: ${date}`,
      `Henkilömäärä: ${guests}`,
      "",
      "Toiveet:",
      message || "-",
      "",
      "Ystävällisin terveisin,",
      name
    ].join("\n");

    window.location.href = `mailto:${restaurantEmail}?subject=${encodeURIComponent(subject)}&body=${encodeURIComponent(body)}`;
  });
}

if (feedbackForm) {
  feedbackForm.addEventListener("submit", async (event) => {
    event.preventDefault();

    const isLocalPreview = window.location.protocol === "file:";
    const formData = new FormData(feedbackForm);

    if (!isLocalPreview) {
      try {
        await submitNetlifyForm(feedbackForm);
      } catch {
        alert("Palautteen lähetys ei onnistunut juuri nyt. Voit lähettää palautteen myös sähköpostilla: ravintola@paatelanportti.com");
      }
      return;
    }

    const name = formData.get("name") || "";
    const email = formData.get("email") || "";
    const message = formData.get("message") || "";
    const subject = "Asiakaspalaute Paatelan Portille";
    const body = [
      "Hei Paatelan Portti!",
      "",
      "Haluaisin jättää asiakaspalautteen.",
      "",
      `Nimi: ${name || "-"}`,
      `Sähköposti: ${email || "-"}`,
      "",
      "Palaute:",
      message || "-",
      "",
      "Ystävällisin terveisin,",
      name || "Asiakas"
    ].join("\n");

    window.location.href = `mailto:${restaurantEmail}?subject=${encodeURIComponent(subject)}&body=${encodeURIComponent(body)}`;
  });
}

if (chatForm && chatMessage) {
  chatForm.addEventListener("submit", (event) => {
    event.preventDefault();

    const message = chatMessage.value.trim();
    if (!message) {
      chatMessage.focus();
      return;
    }

    const text = `Hei Paatelan Portti! ${message}`;
    const whatsappUrl = `https://wa.me/${restaurantWhatsAppNumber}?text=${encodeURIComponent(text)}`;

    window.open(whatsappUrl, "_blank", "noopener");
    chatMessage.value = "";
  });
}
