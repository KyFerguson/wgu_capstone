function renderBarChart(ctx, data, canvas) {
    const months = data.map(entry => entry.date);
    const consumptionValues = data.map(entry => entry.consumption);

    const barWidth = 30;
    const spacing = 20;
    const maxConsumption = Math.max(...consumptionValues);

    ctx.fillStyle = "#3498db"; // Blue color for bars

    for (let i = 0; i < data.length; i++) {
        const barHeight = (consumptionValues[i] / maxConsumption) * (canvas.height - 20);
        const x = i * (barWidth + spacing);
        const y = canvas.height - barHeight;

        ctx.fillRect(x, y, barWidth, barHeight);

        // Draw labels
        ctx.fillStyle = "#333";
        ctx.font = "12px Arial";
        
        const labelX = x + barWidth / 2;
        const labelY = canvas.height - barHeight - 5;

        ctx.fillText(months[i], labelX, labelY);
    }
}

// Example data from the server/API
const serverResponse = [
    { cardType: "heroBanner", backgroundImage: "visit.jpg", title: "Alert!", content: "But I must explain to you how all this mistaken idea of denouncing pleasure and praising pain was born and I will give you a complete account of the system, and expound the actual teachings of the great explorer of the truth, the master-builder of human happiness. No one rejects, dislikes, or avoids pleasure itself, because it is pleasure, but because those who do not know how to pursue pleasure rationally encounter consequences that are extremely painful.", cta: {ctaURL: "www.google.com", ctaContent: "Click here to read details"} },
    { cardType: "heroBanner", backgroundImage: "visit.jpg", title: "Alert!", content: "There is a dog coming to fix your pipes" },
    { cardType: "nav", navItems: [
        { label: "Home", url: "/home" },
        { label: "About", url: "/about" },
        { label: "Services", url: "/services" },
        { label: "Contact", url: "/contact" }
    ]},
    { cardType: "accountInfo", leftTitle: "Ky Ferguson", rightTitle: "Water Service", leftSubtitle: "Next bill due: 2024-03-15", rightSubtitle: "$100.00" },
    { cardType: "picContent", images: ["lemons.jpg"], links: [, "#promo3"], content:"Use your city tap water for a nice lemon bath!" },
    { cardType: "accountInfo", leftTitle: "$100.00", rightTitle: "Pay now", leftSubtitle: "Next bill due: 2024-03-15", rightSubtitle: "" },
    { cardType: "usageHistory", data: [
        { date: "2024-03-01", consumption: 120 },
        { date: "2024-03-02", consumption: 150 },
        { date: "2024-03-03", consumption: 100 },
        { date: "2024-03-04", consumption: 99 },
        { date: "2024-03-05", consumption: 127 }
    ]}  
];

// Function to render cards based on server response
function renderCards(response) {
    const appElement = document.getElementById("app");

    response.forEach(cardData => {
        const cardElement = document.createElement("div");
        cardElement.classList.add("card", `card-type-${cardData.cardType}`);

        switch (cardData.cardType) {
            case "accountInfo":
                cardElement.innerHTML = `
                    <div class="${cardData.leftTitleClass}">
                        <h2>${cardData.leftTitle}</h2>
                    </div>
                    <div class="${cardData.leftSubtitleClass}">
                        <p>${cardData.leftSubtitle}</p>
                    </div>
                    <div class="${cardData.rightTitleClass}">
                        <h2>${cardData.rightTitle}</h2>
                    </div>
                    <div class="${cardData.rightSubtitleClass}">
                        <p>${cardData.rightSubtitle}</p>
                    </div>`;
                break;
            
                case "heroBanner":
                    cardElement.innerHTML = `
                        <div class="hero-banner-container backgroundImage" style="background-image: url('${cardData.backgroundImage}')">
                            <div class="hero-content">
                                <h1>${cardData.title}</h1>
                                <p>${cardData.content}</p>
                                ${cardData.cta ? `<a href="${cardData.cta.ctaURL}" class="cta-button">${cardData.cta.ctaContent}</a>` : ''}
                            </div>
                        </div>`;
                    break;
                
            
            case "picContent":
                cardElement.innerHTML = `
                    <div class="pic-content-container">
                        <img src="${cardData.images[0]}" alt="Image" style="max-width: 100%; height: auto;">
                        <p>${cardData.content}</p>
                    </div>`;
                break;

            case "nav":
                cardElement.innerHTML = `
                    <div class="nav-container">
                        ${cardData.navItems.map(item => `<button onclick="window.location.href='${item.url}'">${item.label}</button>`).join("")}
                    </div>`;
                break;


            case "usageHistory":
                // Render bar chart
                const usageCanvas = document.createElement("canvas");
                usageCanvas.width = 400; // Adjust the width as needed
                usageCanvas.height = 200;
                cardElement.appendChild(usageCanvas);
            
                const usageCtx = usageCanvas.getContext("2d");
                renderBarChart(usageCtx, cardData.data, usageCanvas);
                break;
    }

        appElement.appendChild(cardElement);
    });
}

// Combined window.onload function
window.onload = function () {
    renderCards(serverResponse);
};
``
